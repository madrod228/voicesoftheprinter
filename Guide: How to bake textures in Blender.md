These following instructions will teach how to bake Textures in blender when you have model with multiple textures.

First You will need these 3 things open in Blender

3D Viewport, UV Editor, and Shader Editor.
![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/faf9eb0b-e4bb-426d-9aea-ff865acc3d88)

Now the first thing to do  when you want to Bake a texture is make another UV Map. This will keep the original UV Map so that the textures can be properly baked into the single texture. This will have to be done for every Mesh that is part of the model.
![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/96ede5a2-74af-4565-8a68-94e68c655983)

Simply pressing this button will make an exact copy of the original UV map. Make sure you have the copy selected when you're going to bake. You do not need to give it a special name, but if you give it a name make sure every Mesh has a UV Map of the same name.

![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/04b197c2-70f3-4001-9ea3-1ada6da75742)

Now in the Shader Editor you will need to make a new image texture. It does not need to be connected to anything it simply needs to be there.
![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/4ceca1da-b929-403c-8670-15e931609482)

Now you need to make a new Image with the Image texture you just made for the size of the image I recommended this for the best quality bake.

![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/b848c9d9-e2e7-4e67-8122-c97dc5333710)

You do not need to make a special name for this, but this image texture needs to be placed in every Materials under Shader editor. Because this model im using only has 3 materials it will show the texture being in 3 different Materials with that 3 next to the name. Make sure to select it as well, It will have a white border when selected.

![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/643689f0-686b-4e2a-b4e5-7a996f0ba55b)

Now you're gonna want to select every Mesh that you put your new UV in and open the edit mode in the 3D Viewport.

![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/5cccad32-e93c-4680-bbca-fc4b5800fa52)

Now you're going to open the Select menu and You are going to press Select All.

![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/0e8fe517-b272-4b71-8297-d3dfb36252ef)

Move over to the UV Editor and you're going to do the same exact thing and select all. After you do that you are going to want to hover over UV and go to UV Unwrap and do a Smart UV Project.

![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/a24d847d-9d5d-47e9-bee5-6a451ab93f5e)

These are the settings I recommended for the Smart UV Project.

![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/a14eab1c-7ad5-486b-865b-e0c8d440893f)

Once you press that you should have no Overlapping UVs and they should all be seperated by a little bit.

![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/8d43d1da-be5e-4710-ac6c-a647898d1c94)

The next step is going to Render and choosing Cycles as your option for a Render Engine. You can use your CPU or GPU for the device.

![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/bf6e14d2-006d-4ec4-930c-c286d100b7b4)

Afterwords you need to scroll down to Bake in the Render options. For Bake type choose Diffuse as the type. Make sure you tick Direct and Indirect off before you bake. Those options are for lighting and will mess up the final product.

![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/f4ea1dd8-3f59-441f-880d-f6102cab33f9)

Press Bake and Blender will begin combining the textures into one. This will take some time however, but not very long. After the baking is done you will have all the textures in one image.

![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/99dacc38-94ad-49ad-bc0c-1b996e46c271)

To save this Image just go up to Image and select save or save as.

![image](https://github.com/madrod228/voicesoftheprinter/assets/9602000/098d47f5-fd94-40f6-99ee-f77f82bf1ec0)

Then you have it the complete texture for your model. Make sure you export your model with Materials otherwise it will try to use non existant textures to put on the model.
