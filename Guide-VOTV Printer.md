# VotV 3D Printer a rough Guide
  - 1 Meter in Blender = 1 Centimeter in VotV/UE4
  - ## Naming norms for the Printer
    - model_name_example``.obj``  
    - ``diffuse_``model_name_example``.png``
    - ``pbr_``model_name_example.``png``
    - ``normal_``model_name_example``.png``
    - ``emissive_``model_name_example``.png``
  - ## Update 0.8.0 Note
    Update 0.8.0 changed the naming scheme for textures, so for any older models that you want to print make sure to move the texture type to the back of the filename as shown above instead of at the front of the filename. 
  
  - ## N-Gons and Vert Count

    - ### !!QUIRK!! Vert count being 3x-3.5x more than in Blender <br>
    UE4 the engine VotV runs on for some reason **triples** the Vert count. Its a Quirk that is Not fixable. (or no solution has been Found.) <br>
    It's recommended to *auto Quad* or *manually Quad* everything before exporting on Models that are primarily Tri's. <br>
    Blender sees 2 Tri's that make up a Quad as 4 Verts therefore showing less Vert's in the Status of the model in Blender. <br>
    The Printer does not, and will usually show ~50% more Vert's in its Menu as 2 Tri's = 6 Vert's

    - Try to not have any N-Gons. N-Gons are Faces of a Mesh that have more than ``4 Vertices``. <br>
      Unreal Engine pokes Faces with more than 4 Vert's for some reason instead of triangulating the Faces, creating the mess below
      ![pokerfacelowq](https://github.com/madrod228/voicesoftheprinter/assets/93410850/a0cf1b7d-d55b-4c07-a379-cda6679a8484) <br>
      to have an easy fix, tick this on Export (or Triangulate manually before exporting) <br>
      ![triangulat](https://github.com/madrod228/voicesoftheprinter/assets/93410850/4f2741e7-7e33-4c66-8d01-9681c99b6df1) <br>
      its an easy "fix" button but will increase the Vert count by ~50%. ontop of the 3x from UE4 lol.<br>
      Pretty useful if you dont know how to retopo and just want it in the game. <br>
      What it does exactly is ``1 Quad -> 2 Triangles -> 6 Verts, N-Gons can turn into alot of Tri's, execpt alot more Vert's``



  - ## Collider Shenanigans
    - ### What does Convex Hull do/mean? <br>
        Convex Hulls are use for "Simplified" and faster Collision checks. <br>
	VotV usually generates one out of the ``0.6.3 Single Visual one or the Objects after`` **/** ``0.7.0 the UCX_ Prefixed Objects`` <br>
	its recommended to Convex Hull them yourself so it doesnt have todo it everytime you load into a Save. <br>
	So what happens if you dont make a custom Collider? <br> <br>
	This will happen, VotV will use the entire Mesh to generate a Convex Hull <br>
 	making a huge slope in the progress and closing off the bottom of the chair <br>
	![badcollider](https://github.com/madrod228/voicesoftheprinter/assets/93410850/9ba5f1bb-2070-47a6-ac2f-f483c3a2e5e6)

    	You can Duplicate the Object and then seperate parts of it into their own Objects to create a more accurate Collider. <br>
 	![goodcollider](https://github.com/madrod228/voicesoftheprinter/assets/93410850/a4cf72f4-def5-459f-8327-a4a46a182d03)

    - ### Current Pre-Alpha 0.7.0 (pa07_0005) and afterwards*
      - **All** ``Colliders`` require the ``UCX_`` prefix
	  - there needs to be minimum ``1 Collider``

	- ### Pre-Alpha 0.6.3 (pa063b_0003) and below
		- the first created ``Object`` is both ``Visual`` and a ``Collider``
		- Any additonal ``Object`` will turn the ``First Object`` into being **``Visual only with no Collider.``** <br>
	  Any additonal ``Object`` will therefore turn into a **``Collider.``**
	  - If your model only prints one of the Colliders, ``duplicate all colliders and delete the old ones`` this will move the ``Object`` you want to be ``Visual`` to the beginning of the ``.obj`` file.

- ## Textures
  - All Texture files [.png] are optional
    - but will result into Warning about missing Textures
  - **BitDepth** that is above 32 in the windows propeties menu will crash the game <br> 
  (check via RightClick (png) > Properties > Details)
  - **``UV's Vertexes too close or on the edge(s)``** (aka 0/1 in coordinates) <br> 
  *can* glitch the textures out since the Printer/VotV/Unreal does not repeat Textures.
  - ### **there can only be 1 material**
    - Pre-Alpha 0.7.0 (pa07_0005)
      - It will might print but throw warnings
    - Pre-Alpha 0.6.3 (pa063b_0003)
      - if multiple are present it will only print the first one and ignore all others
  -  ### ``diffuse_model_name_example.png`` 
      - is the Color/Diffuse and the Alpha/Transparency (on )
      - **Alpha/Transparency are clipped** when the transparency goes below 107/255 it will start to clip. to Mimic how VotV displays Alpha <br>
	   go to ``Properties``>``Material``>``Viewport Display`` and set ``Blend Mode`` to ``Alpha Clip`` then set ``Clip Threshold`` to 0.33
  - ### ``pbr_model_name_example.png`` PBR Channels
      - Red Channel = Metallic
	  - Green Channel = Specular
	  - Blue Channel = Roughness
	  - Alpha Channel = Alpha (up to version 061, not needed anymore on/after 062)
  - ### ``normal_model_name_example.png`` Normal Map
    - VotV/Unreal Engine uses the DirectX Normal Map format <br>
	if your model looks a bit uncanny fix it by **``inverting/flipping the Green Channel``**
	- if you want to get rid of the normal map message make a blank 16x16 ``normal_model_name_example.png`` that has rgb(128,128,255) as a single color

### [How to create PBRs by Xiphi](https://www.youtube.com/watch?v=1knCUpq7Yz0&t)
![dsad](https://github.com/madrod228/voicesoftheprinter/assets/9602000/d2af6236-e5d3-4aae-8e22-75eccd2d1ea4)
### [How to make 3D Prints for VOTV by Xiphi](https://www.youtube.com/watch?v=aL-fLuwMXTo)
![hq720](https://github.com/madrod228/voicesoftheprinter/assets/9602000/595308a8-4e09-4141-8ae6-5996a2a969bc)
