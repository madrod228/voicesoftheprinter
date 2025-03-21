# VotV 3D Printer a rough Guide
 This file is for 0.8 and up only. see commit history of this file to view older versions \
 Things to never forget \
 1 Meter (1m) in Blender (Default settings) = 1 Centimeter (1cm) in VotV
 

  - ## File Structure
    The Printer has 2 Folder/Naming Scheme’s you can use which also affects how you make the Model. \
    Be it the more size friendly Single Material. Or the lazy Multi Material approach. \
    It is required that the ``.obj and .mtl`` name is the same as the folder name, or the other way around. \
    So the game can regonize it exists.
    - Single Material Method \
      Usually requires the user to bake all Objects into 1 Texture and merge all Objects into a Single one.
      - Folder_name
        - Folder_name``.obj``
        - diffuse_Folder_name``.png``
        - pbr_Folder_name``.png``
        - normal_Folder_name``.png``
        - emissive_Folder_name``.png``
      
    - Multi Material \
      It can be done quick and cheap at the cost of filesize if its a big Model with many big Textures.\
      The maximum materials that can be used is ~64. \
      **try to not have spaces in the folder/file name.** If not followed, it will create issues.
      - Folder_name
        - Folder_name``.obj``
        - Folder_name``.mtl``
        - diffuse_material_name``.png``
        - diffuse_material_name_1``.png``
        - pbr_material_name``.png``
        - normal_material_name``.png``
        - emissive_material_name``.png``

- ## Textures and Properties.cfg
  - All Texture files [.png] are optional
    - but will result into Warning about missing Textures
    - **BitDepth** that is above 32 in the windows propeties menu will crash the game \
      (check via RightClick (png) > Properties > Details)
  - ###  properties.cfg
    - This file will generate after clicking on the Model Preview in the Printer UI. \
      It stores values for 4 features
      1. ``filter_`` 0-1, aka on or off, all it does is render the texture with **Billnear Smoothing**
      2. ``physical_material`` 0-15
         ```
         0 - default , 1 - wood , 2 - metal , 3 - concrete , 4 - rubber , 5 - paper , 6 - hollow metal , 7 - flesh , 8 - plush , 9 - metal2 , 10 - pinecone , 11 - glass , 12 - cardboard , 13 - heavy metal , 14 - no sound , 15 - rubber2
         ```
      3. ``emissive_strength`` 0-inf
      4. ``is_lamp`` 0-1, off-on, lets you add a light into the model with these values set as default
         ```cfg       
          is_lamp=0
          lamp_color=(R=1,G=1,B=1)
          lamp_offset=(X=0,Y=0,Z=0)
          lamp_intensity=5000
          lamp_attenuation=2500
          lamp_shadows=0
         ```
  - ### ``diffuse_folder_name.png / diffuse_material_name.png`` 
      - **Alpha/Transparency are clipped** when the transparency goes below 107/255 it will start to clip. to Mimic how VotV displays Alpha \
	   go to ``Properties``>``Material``>``Viewport Display`` and set ``Blend Mode`` to ``Alpha Clip`` then set ``Clip Threshold`` to 0.33
  - ### ``pbr_folder_name.png / pbr_material_name.png`` PBR Channels 
    still unsure if the game reads the brightness of the files wrong, cross refrencing blender to game it seems to be fixed past 0.8
    - Red Channel = Metallic
    - Green Channel = Specular
    - Blue Channel = Roughness
  - ### ``normal_folder_name.png / normal_material_name.png`` Normal Map 
    - still unsure if the game reads the brightness of the files wrong, cross refrencing blender to game it seems to be fixed past 0.8
    - VotV/Unreal Engine uses the DirectX Normal Map format \
      if your model looks a bit uncanny fix it by **``inverting/flipping the Green Channel``**
  - ### ``emessive_folder_name.png / emessive_material_name.png`` Emessive
    - Makes parts glow on prints, works the same way as in blender, configure emissive strength in the properties.cfg

  - ## Colliders
    - VotV by Default Convex Hull's the Print if there are no custom colliders present. \
      Meaning anything Concave Shape will be gone. \
      to create a collider, create a object and add the prefix ``UCX_``. it is Recommended to create them. \
      Since on **every startup of the savefile** it will run the Convex Hull thing.
      Examples below on how it would affect Print's
      \
      \
      Left in checkerboard is the custom colliders \
      around 40 of them since the object is a bit complex and time was put into it \
      you could also just make it very simple, aka 4 sloped walls and the flat bottom.
      ![colliderrr](https://github.com/user-attachments/assets/2ddfdd68-bba2-4ea2-bbc6-6641d19422db) \
      on the right is with no colliders, what the game does when there is no collider given.

- # Issues?
  - ### Try to not have any N-Gons. N-Gons are Faces of a Mesh that have more than ``4 Vertices``. <br>
      Unreal Engine pokes Faces with more than 4 Vert's for some reason instead of triangulating the Faces, creating the mess below
      ![pokerfacelowq](https://github.com/madrod228/voicesoftheprinter/assets/93410850/a0cf1b7d-d55b-4c07-a379-cda6679a8484) <br>
      to have an easy fix, tick this on Export (or Triangulate manually before exporting) <br>
      ![triangulat](https://github.com/madrod228/voicesoftheprinter/assets/93410850/4f2741e7-7e33-4c66-8d01-9681c99b6df1) <br>
      its an easy "fix" button but will increase the Vert count by ~50%. ontop of the 3x from UE4 lol.<br>
      Pretty useful if you dont know how to retopo and just want it in the game. <br>
      What it does exactly is ``1 Quad -> 2 Triangles -> 6 Verts, N-Gons can turn into alot of Tri's, expect alot more Vert's``

  - ### Texture streching 
    This is caused by Floating point issues in UE4 addon being used and the UV \
    ![image](https://github.com/user-attachments/assets/35fe0c89-b6fb-4730-b84b-952d790293b4) \
    To fix it *easily* i recommend to Select the entire UV and move it by 1 in X or Y or both at the same time. \
    so the UV is not on the grid anymore but off by 1 or 2.
    ![image](https://github.com/user-attachments/assets/c2909efa-f800-49e8-b7be-0c228c6e51ad) \
    The Second recommended fix is making the UV smaller by 1-3%.
   
  - ## Vert Count increase Research
    - ### Vert count being 3x-3.5x more than in Blender <br>
    UE4 the engine VotV runs on for some reason **triples** the Vert count. Its a Quirk that is Not fixable. (or no solution has been Found.) <br>
    It's recommended to *auto Quad* or *manually Quad* everything before exporting on Models that are primarily Tri's. <br>
    Blender sees 2 Tri's that make up a Quad as 4 Verts therefore showing less Vert's in the Status of the model in Blender. <br>
    The Printer does not, and will usually show ~50% more Vert's in its Menu as 2 Tri's = 6 Vert's


<br><br>

### [How to create PBRs by Xiphi](https://www.youtube.com/watch?v=1knCUpq7Yz0&t)
![dsad](https://github.com/madrod228/voicesoftheprinter/assets/9602000/d2af6236-e5d3-4aae-8e22-75eccd2d1ea4)
### [How to make 3D Prints for VOTV by Xiphi](https://www.youtube.com/watch?v=aL-fLuwMXTo)
![hq720](https://github.com/madrod228/voicesoftheprinter/assets/9602000/595308a8-4e09-4141-8ae6-5996a2a969bc)
