# *Project: New Light City*

<img src="Images\ProjectNLC1.gif" width="100%"/>

[Trailer](https://www.youtube.com/watch?v=jPAzV-djFh0)  

Worked as **Gameplay Programmer**  
*2020 - 2021*

This was a project me and a friend started working on late 2020. It was my first working in Unreal Engine and with C++. Our goal was to do a demo and try and find funding to continue the development. The first demo was completed, but we never had the opportunity to pick up the development again. However, I still want to showcase it here since I'm quite proud of several of the features that we implemented, I feel that they showcase my strong C++ and Unreal Engine experience that has only gotten since then.

## Gameplay

<table>
  <tr>
	<td width="50%"><img src="Images\ProjectNLC2.gif" /></td>
	<td width="50%"><img src="Images\ProjectNLC3.gif" /></td>
  </tr>
  <tr>
	<td width="50%"><img src="Images\ProjectNLC4.gif" /></td>
	<td width="50%"><img src="Images\ProjectNLC5.gif" /></td>
  </tr>
  <tr>
	<td width="50%"><img src="Images\ProjectNLC7.gif" /></td>
	<td width="50%"><img src="Images\ProjectNLC8.gif" /></td>
  </tr>
</table>

**What I worked on:** 
- A fully functional chess game done entirely in C++.
- Journal system with unlockable entries.
- Multiple choice dialog system.
- Noise/sound based stealth detection system.
- True first person controller coded from scratch in C++.
- AI behavior tree for enemies and robots.
- Animation Blueprint and blending.
- Traffic system.
- Technical art implementation and solutions.

<br/>
<td width="50%"><img src="Images\ProjectNLC6.gif" /></td>
<details>
<summary>Code Example:</summary>
Here is a method that returns true or false if the move that is being checked will put your own king in check.

What I do here is simulate the movement of all your pieces, and for each movement I also simulate if this move will enable any of the opponents pieces to attack the kings tile when it's their turn. If so I remove that move from the array of possible moves. (Gif of trying to move piece that defends king).

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


**Tools I worked with:** 
- Unreal Engine C++ and Blueprints.