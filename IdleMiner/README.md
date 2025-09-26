# *Idle Miner*

<img src="Images\IdleMiner13.gif" width="80%"/>

Worked as **Game Programmer**  and **Game Designer**\
*2025 January 13 - 2025 February 28*

This game was developed during a solo assignment at Yrgo, we where tasked to make a mobile game in Unity with the optional challenge to include Firebase database system for online functionalities like saving or multiplayer. I decided to redo a prototype I did back in 2021 but for mobile and with some multiplayer functionality. The game is an idle game about mining ore from asteroids in space, it is heavily inspired by EVE Online's mining gameplay. In short, the game is about clicking an asteroid and watching your ship mine it slowly, as you mine, buy and use your upgrades stratigically.

## Gameplay

<table>
  <tr>
    <td width="35%"><img src="Images\IdleMiner10.gif"/></td>
    <td width="35%"><img src="Images\IdleMiner8.gif"/></td>
  </tr>
</table>

**What I worked on:** 
- Game Design.
- Online functionality.
- Flexible upgrade system.
- Deteriorating asteroids.
- Modeling Voxels.
- Sound effect and implementation. 
- Technical art implementation and solutions.

## Upgrade cost system:
<td width="35%"><img src="Images\IdleMinerProgression.png"/></td>

Since the player's power increase exponentially I needed to create an efficient way of tweaking the upgrade costs, so I developed this upgrade cost system. It requires a minimum of one specified upgrade bracket, you define the base costs and the "power of" which will be multiplied by the ability's current level. This works pretty well by itself, if necessary you can tune the cost by adding more level brackets. The brackets are stored in a scriptable object for independent adjustments from the corresponding ability. The scriptable objects can then be assigned to the desired ability's upgrade bracket reference field. All the abilities inherit from the base class Ability.cs, which implements the method to calculate the ore cost. When an ability reaches a brackets end level it will look for the next one in the scriptable object. If it does not exists it will continue to use the last one in the list indefinetily, enabling infinite levels with the possibility of manual cost balancing.

<details>
<summary>Scriptable object:</summary>

```
[CreateAssetMenu(fileName = "CostBracketsObject", menuName = "ScriptableObjects/CostBracketScriptableObject", order = 1)]
public class CostBracketScriptableObject : ScriptableObject
{
    [SerializeField]
    public List<CostBracket> costBrackets = new ();
}

[Serializable]
public class CostBracket
{
    [SerializeField] public int endLevel = 0;
    [SerializeField] public float oreBaseCost = 0;
    [SerializeField] public float blueBaseCost = 0;
    [SerializeField] public float powerOf = 0;
}
```
</details>

<details>
<summary>Calculate ore cost:</summary>

```
public float CalculateOreCost(int targetLevel, CostBracketScriptableObject costBracketScriptableObject)
    {
        CostBracket costBracket = IdentifyNextBracket(targetLevel, costBracketScriptableObject);
        float cost = 0;
        if (costBracket == null)
        {
            return cost; // if 0 is returned invalidate results.
        }

        var powerOfCalc = costBracket.oreBaseCost * Mathf.Pow(targetLevel, costBracket.powerOf);

        cost = powerOfCalc;

        return cost;
    }
```
</details>

<details>
<summary>Identify next bracket:</summary>

```
    CostBracket IdentifyNextBracket(int targetLevel, CostBracketScriptableObject costBracketScriptableObject)
    {
        foreach (CostBracket costBracket in costBracketScriptableObject.costBrackets)
        {
            if (costBracket.endLevel >= targetLevel)
            {
                return costBracket;
            }
        }
        // if no valid costbracket for targeted level exists return the latest/last one for infinite upgrades.
        return costBracketScriptableObject.costBrackets[costBracketScriptableObject.costBrackets.Count() - 1];
    }
```
</details>

<br>

### Asteroid Deteriorating Timelapse:
<img src="Images\IdleMiner12.gif" width="30%" />
A timelapse of an asteroid being mined down to it's core, breaking down over time.

<br>

## How gameplay evolved:
The gameplay evolved quite a bit from the prototype, originally you tap an asteroid to start mining, tap the screen to mine faster and buy upgrades to improve your mining lasers. In this re-imagined version I added the ability to control your ship, making it orbit an asteroid or even fly over to another player. This movement has zero effect on the mining, but it's nice to be able fly around and look at some of your co-miners while mining! One big design change I ended up doing was taking away the ability to tap to mine, as this never matched the feel I wanted the game to have. It was not supposed to be about tapping the screen as fast as possible to mine at lightning fast speeds. So I removed this functionality. When I removed it, it opened up the time and for players to use abilites and plan their upgrades better. This perfecftly represented the feel I was going for; chill atmospheric space mining. The game also gained complexity in other parts. Now mining from the same asteroids as other players you would gain a bonus. I added functionality that made asteroids gradually break down and parts of different rarity will break off, you can then tap any of these pieces to gain ore instantly. Another mechanic I added was a time based mini game, it will start when an asteroid core is exposed. You gain a rare ore mining multiplier relative to how much you mined from the core. The player should want to spend their cooldowns when a core is exposed. The final layer of complexity comes from the explosion of the core, spawning core pieces that you can directly tap to gain the rare ore.

<table>
  <tr>
    <td width="35%"><img src="Images\IdleMiner4.gif"/></td>
    <td width="35%"><img src="Images\IdleMiner2.gif"/></td>
  </tr>
</table>

**Tools I worked with:** 
- Unity C#
- Firebase
- VS Code
- Blender
- Magica Voxel
- Audacity
