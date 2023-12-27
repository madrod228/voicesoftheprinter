
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
