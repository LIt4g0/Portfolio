# *Code samples:*

Most code samples here will refer to game projects, but some are separate samples. 

## Upgrade cost system:
<td width="35%"><img src="Images\IdleMinerProgression.png"/></td>

Language: C#\
Engine: Unity\
Project: [***Idle Miner***](/IdleMiner#mr-Idle-Miner)

For an idle incremental game I needed to create an efficient way of tweaking the upgrade costs, so I developed this upgrade cost system. It requires a minimum of one specified upgrade bracket, you define the base costs and the "power of" which will be multiplied by the ability's current level. This works pretty well by itself, if necessary you can tune the cost by adding more level brackets. The brackets are stored in a scriptable object for independent adjustments from the corresponding ability. The scriptable objects can then be assigned to the desired ability's upgrade bracket reference field. All the abilities inherit from a base class which implements the method to calculate the ore cost. When an ability reaches a brackets end level it will look for the next one in the scriptable object. If it does not exists it will continue to use the last one in the list indefinetily, enabling infinite levels with the possibility of manual cost balancing.

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

## Check mate solution:
<br/>
<td width="50%"><img src="Images\ProjectNLC6.gif" /></td>

Language: C++\
Engine: Unreal Engine\
Project: [***Project: New Light City***](/ProjectNewLightCity#mr-ProjectNewLightCity)

Here is a method that returns true or false if the move that is being checked will put your own king in check.

What I do here is simulate the movement of all your pieces, and for each movement I also simulate if this move will enable any of the opponents pieces to attack the kings tile when it's their turn. If so I remove that move from the array of possible moves.

<details>
<summary>Code:</summary>

```
bool AChessBoard::IsSelfCheckMove(AChessPiece* SimChessPiece, AChessTile* OriginTile, AChessTile* SimTargetTile)
{
	bSimCheckMate = false;
	bSimSelfCheck = true;

	AChessPiece* TargetedPiece = nullptr;
	if (SimTargetTile->IsOccupied(CurrentTurn))
	{
		TargetedPiece = SimTargetTile->GetOccupyingPiece(CurrentTurn);
	}
	SimChessPiece->TrySetTile(SimTargetTile, CurrentTurn);
	UpdateTurn();

	if (bWhiteTurn)
	{
		for (AChessPiece *ChessPiece : WhitePieces)
		{
			SetAvailableMovementTiles(ChessPiece->CurrentTile, CurrentTurn);
		}
	}
	else
	{
		for (AChessPiece *ChessPiece : BlackPieces)
		{
			SetAvailableMovementTiles(ChessPiece->CurrentTile, CurrentTurn);
		}
	}

	SimChessPiece->TrySetTile(OriginTile, CurrentTurn - 1);
	ResetTurnTo(CurrentTurn - 1);
	if (TargetedPiece)
	{
		ReactivatePiece(TargetedPiece, SimTargetTile);
	}

	bSimSelfCheck = false;

	if (bSimCheckMate)
	{
		UE_LOG(LogTemp, Warning, TEXT("Move removed as it does put king in Check!"));
		bSimCheckMate = false;
		return true;
	}
	else
	{
		UE_LOG(LogTemp, Warning, TEXT("Move does not put king in Check."));
		bSimCheckMate = false;
		return false;
	}
}
```
</details>



## More to come!