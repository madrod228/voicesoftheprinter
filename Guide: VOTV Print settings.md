# VotV 3D Printer a rough Guide
  - ## Object/Mesh and Collider Creation
    - 1m in Blender = 1cm in VotV
	  - or if your brain is misfunctioning <br> 1 meter **IN BLENDER** -> 1 centimeter **IN UNREAL** (also know as voices of the void, the game youre trying to add the model to have it printable)
    - the first created ``Object`` is both ``Visual`` and a ``Collider``
    - Any additonal ``Object`` will turn the ``First Object`` into being **``Visual only with no Collider.``** <br>
	Any additonal ``Object`` will therefore turn into a **``Collider.``**
	- example of ``Visual/Colliders`` is [here](https://i.imgur.com/M8WnIPY.png). <br>
	🟩Green was created first, 🟦Blue and 🟥Red last. <br>
	Due to that Items can clip into the 🟩Green where there is no Collider.
	- If your model only prints one of the Colliders, ``duplicate all colliders and delete the old ones`` this will move the ``Object`` you want to be ``Visual`` to the beginning of the ``.obj`` file.
  - ## Collider Shenanigans
  - **``Every Collider will get Convex Hull'ed when imported.``** <br> To see what it does or how to do it in blender yourself see [this gif](<https://i.imgur.com/LfFiwbi.gif>).
  - [this image](<https://i.imgur.com/M8WnIPY.png>) also shows that the 🟥Red Collider got Convex Hull'ed therefore the Board can lean onto thin Air. <br> Same thing is with the 🟦Blue Object, Batteries can Hover on Nothing.
  - if you have Arches similar to [this gif](<https://i.imgur.com/1jGOhZi.gif>) the game/UE will poke it  **creating the mess at the end of the gif**. <br> Triangulate the mesh with export settings or before exporting to avoid it.
  - **``UV's Vertexes too close or on the edge(s)``** (aka 0/1 in coordinates) *can* glitch the textures out since the Printer/VotV/Unreal does not repeat Textures.

- ## Naming norms for the Printer
  - model_name_example``.obj``
  - model_name_example``.png``
  - model_name_example``_pbr.png``
  - model_name_example``_normal.png``
	
- ## Textures
  - ### All Texture files [.png] are optional
    - but will result into Warning about missing Textures
  - **BitDepth** that is above 32 in the windows propeties menu will crash the game (check via RightClick > Properties > Details)
  - ### **there can only be 1 material**
    - if multiple are present it will only print the first one and ignore all others
  -  ### ``model_name_example.png`` 
      - is the Color/Diffuse and the Alpha/Transparency
      - **Alpha/Transparency are clipped** when the transparency goes below 107/255 it will start to clip, to Mimic how VotV displays Alpha go to ``Properties``>``Material``>``Viewport Display`` and set ``Blend Mode`` to ``Alpha Clip`` then set ``Clip Threshold`` to 0.33
  - ### ``model_name_example_pbr.png`` PBR Channels
      - Red Channel = Metallic
	  - Green Channel = Specular
	  - Blue Channel = Roughness
	  - Alpha Channel = Alpha (up to version 061, not needed anymore on/after 062)
  - ### ``model_name_example_normal.png`` Normal Map
    - VotV/Unreal Engine uses the DirectX Normal Map format, if your model looks a bit uncanny fix it by **``invert/flip the Green Channel``**
	- if you want to get rid of the normal map message make a blank 16x16 model_name_example_normal.png that has rgb(128,128,255) as a single color

### [How to create PBRs by Xiphi](https://www.youtube.com/watch?v=1knCUpq7Yz0&t)
![dsad](https://github.com/madrod228/voicesoftheprinter/assets/9602000/d2af6236-e5d3-4aae-8e22-75eccd2d1ea4)
### [How to make 3D Prints for VOTV by Xiphi](https://www.youtube.com/watch?v=xKyMyZzdjSk)
![hq720](https://github.com/madrod228/voicesoftheprinter/assets/9602000/595308a8-4e09-4141-8ae6-5996a2a969bc)
