
- requirements
  - 1m in blender = 1cm ingame
  - every object needs a number prefix or can just be the number (number only is perfeered tho, seen issues with it being a prefix)
  - ``0`` should be the main mesh
  - ``1,2,3``+ should be used for collision
  - every collision box will get convex hull'ed when imported or if no collision is there, the main model will be convex hull'ed
  - create the collision last or it will mess up the order for some reason

- Naming
  - ``model.obj`` - base model
  - ``model.png`` - color\diffuse\alpha
  - ``model_pbr.png`` - pbr maps (R@255 - metallic,G@255 - Specular ,B@255 - Roughness)
  - ``model_normal.png`` -normal map (directx, if you're rebaking them) 

### all texture files are optional, resulting in a black/pink texture on the model

### [How to create PBRs by Xiphi](https://www.youtube.com/watch?v=1knCUpq7Yz0&t)
![dsad](https://github.com/madrod228/voicesoftheprinter/assets/9602000/d2af6236-e5d3-4aae-8e22-75eccd2d1ea4)
### [How to make 3D Prints for VOTV by Xiphi](https://www.youtube.com/watch?v=xKyMyZzdjSk)
![hq720](https://github.com/madrod228/voicesoftheprinter/assets/9602000/595308a8-4e09-4141-8ae6-5996a2a969bc)
