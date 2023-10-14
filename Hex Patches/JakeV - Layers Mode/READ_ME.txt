Boosters Lab has a LAYERS MODE.
To use it, run the "launch_layers.bat". You need the latest version of BL for this.
Layers "Far Back" and "Back" draw behind the player. Front/Far Front draw in front (revolutionary, I know)

To apply the patch, use boosters lab Actions->Hex patcher and paste the hexpatch.txt into it. It should apply 15 patches.
= Really Important:
 - Back up your EXE before applying the patch!

= Important:
 - Only the FRONT layer has collision
 - <CMP only works with the front layer
  - Boosters lab's "Generate CMP" feature spits out "<CML:layer:x:y:tile_type". But only <CMP is supported currently.
 - Snack blocks use their block texture now (should fix someday)
 - Report any bugs!
 - Should be FAIRLY USABLE with other hacks.
 - Save your maps in BL Layers Mode before loading them in game.
 - Never open BL without layers on your layers project

= Technical
 - This hack changes: InitMapData2, LoadMapData2, ModeAction, ModeOpening, GetAttribute, DeleteMapParts, ChangeMapParts, ShiftMapParts.
 - This hack DELETES PutStage_Front and PutStage_back.
 - It uses "0x4A4EFC" to store 4 bytes. These 4 bytes are a pointer to the 3rd layer.
 - There is lots of unused space near PutStage_Front, since front/back are merged into 1 function

= TODO
 - Replace <CMP with <CML
 - Fix snack block texture
 - Fix snack blocks being a little janky sometimes