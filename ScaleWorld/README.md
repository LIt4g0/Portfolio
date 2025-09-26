# *Scale World*

<img src="Images\ScaleWorld1.gif" width="100%"/>

Worked as **Gameplay Programmer**  
*2025 March - 2025 April*

This game was made during our Unreal Engine course at Yrgo. The assignment was to make a solo game focusing on utilizing the strengths of the Unreal Engine.

I first started prototyping a game where you would jump from mini planet to mini planet, manipulating gravity so that you would be attracted to whichever planet was closest. I had several great ideas and the core mechanic was in place but I decided to focus on making a smaller game instead.
<table>
  <tr>
    <td width="50%"><img src="Images\Planetary1.gif" /></td>
    <td width="50%"><img src="Images\Planetary2.gif" /></td>
  </tr>
  <tr>
    <td width="50%"><img src="Images\Planetary3.gif" /></td>
    <td width="50%"><img src="Images\Planetary4.gif" /></td>
  </tr>
</table>

I decided to make a first person game where you take control of the characters you shoot. Each character you possess is unique in size and mass, this enables you to go places or do things that would not be possible with the other characters. You will have to consider the mass of a characters in order to press down a button or balance multiple characters on a see saw. This all combined into a pretty neat game, I would describe it as a unique and frustratingly challenging but fun puzzle platformer. Utilizing Unreal Engine's strong First Person Perpsective focus and rapid level design tools I was able to build this game in less than a month.

## Gameplay

<table>
  <tr>
    <td width="50%"><img src="Images\ScaleWorld5.gif" /></td>
    <td width="50%"><img src="Images\ScaleWorld6.gif" /></td>
  </tr>
  <tr>
    <td width="50%"><img src="Images\ScaleWorld7.gif" /></td>
    <td width="50%"><img src="Images\ScaleWorld8.gif" /></td>
  </tr>
  <tr>
    <td width="50%"><img src="Images\ScaleWorld9.gif" /></td>
    <td width="50%"><img src="Images\ScaleWorld10.gif" /></td>
  </tr>
  
</table>


**What I worked on:** 
- Game Design.
- Level Design.
- Implemented a system for swapping characters with different scales.
- Implemented a spawning system.
- Physic based seesaw mechanics.
- Mass conditional button and door system.
- Check point system.
- Quick Save and Load system.
- Materials and Niagara Particles.

## Checkpoint system:
<td width="35%"><img src="Images\SaveOverview.png"/></td>

Since the game is quite rage inducing when you die I decided to implement a checkpoint system. It was later expanded upon to enable quick saves and reloads as well. The checkpoints are placed at specific points in the game and will ensure you will restart at the beginning of the current puzzle with every object reset to the position and state they were in at that time. It could still be improved upon, but as blueprints go I'm pretty satisfied with the functionality and readability.

<details>
<summary>Assign and save prep</summary>

<td width="35%"><img src="Images\AssignAndSaveprep.png"/></td>
</details>

<details>
<summary>Save all:</summary>

<td width="35%"><img src="Images\SaveAll.png"/></td>
</details>

<details>
<summary>Load prep:</summary>

<td width="35%"><img src="Images\ReloadPrep.png"/></td>
</details>

<details>
<summary>Load all:</summary>

<td width="35%"><img src="Images\LoadAll.png"/></td>
</details>


**Tools I worked with:** 
- Unreal Engine