# Cagaroo's Tutorials

## About
Welcome! Here is a collection of tutorials for modding _Kingdom Hearts: Dream Drop Distance_ for both the Nintendo 3DS and PC remasters.

## Glossary
* **OpenKH**: an online resource that contains all related information to _Kingdom Hearts: Dream Drop Distance_. 
    * **[Entities](https://openkh.dev/ddd/dictionary/entities.html)**: a resource that lists many of the models in the game. 
* **mod.yml**: Mod instructions PC mods. See OpenKH's [YAML documentation](https://openkh.dev/tool/GUI.ModsManager/creatingMods.html) for more information.
* **meta.json**: Mod instructions for 3DS mods. These can be edited directly in Nightmare Editor.d

## Prerequisites
As for all projects, you should be set up with the appropriate files, programs, and tools! I will list what I have used:

* [OpenKH](https://openkh.dev/ddd/)
* [Nightmare Editor by Solt11](https://github.com/solt-frfr/Nightmare-Editor-AUI/releases) (3DS only)
* [OpenKH.KHModels](https://github.com/OpenKH/OpenKh/releases) by OpenKH + Kite98
* PMO Builder/KH Asset Studio by Kite98
* [KHBBSMesh](https://github.com/thamstras/KHBBSMesh/releases) by Thamstras
* a 3D-modeling program (Blender preferred, but whatever you're comfy with)
* a picture-editing program (Paint.NET, GIMP, Photoshop, etc)
* Extracted game files
  * 3DS:  a game dump of KHDDD (via GodMode9 or Azahar)
  * PC:   extracted files from OpenKH

You are free to structure your modding environment however you like. However, it may be more simple and clean to contain your modding environment within the mods list of either OpenKH or Nightmare Editor. Below are some example directories. 
* Nightmare Editor: `\NightmareEditor\Mods\<modname>`
* OpenKH: `openkh\mods\<authorname>\<modname>`

Mods need to contain the following files in order to function properly.
* **mod.yml**: Mod instructions PC mods. See OpenKH's [YAML documentation](https://openkh.dev/tool/GUI.ModsManager/creatingMods.html) for more information.
* **meta.json**: Mod instructions for 3DS mods. These can be edited directly in Nightmare Editor.
* **icon.png**: A small (minimum: 128 x 128 px) icon used in the OpenKH Mod Manager mod list.
* **preview.png**: A medium (minimum: 512 x 218 px) preview image used in both the OpenKH Mod Manager and Nightmare Editor, when the mod is selected. 

## Game Extraction
To make any type of texture, model, or animation replacements, we will first need to access the source files. This can be done for both consoles the following ways:

### 3DS
1. Ensure you have the 3DS *.rbin files, from dumping the game via either GodMode9 or Azahar. 
2. Using Exam Editor, navigate to the `Nightmare Editor` option. This will bring up a new screen.

![Image](<img/nem0.png>)

3. Click on the magenta `+` icon. This will open a file explorer window. Navigate to the appropriate .rbin file to unpack the file. 
    * This will extract a bunch of files in the order it is officially stored. The naming convention (index prefix and filename) are necessary for repacking later.

![Image](<img/nem1.png>)

### PC
1. Using OpenKH's Mod Manager, navigate to `Settings > Run the Setup Wizard`
2. Ensure Mod Manager has the path for _KINGDOM HEARTS 2.8 Final Chapter Prologue_

![Image](<img/okh1.png>)

3. `(Optional)` Install LuaBackend and enable Direct Launching, these make loading and testing mods quicker.
4. On `Extract Game Data`, select Dream Drop Distance.
    * Ensure you have at least 19 GB of storage!
    * `(Optional)` You may also declare a path for the extracted files. By default it will choose the "extract" folder relative to the Mod Manager.

![Image](<img/okh2.png>)

From this point forward, all sections will assume you have the game files already extracted. 

**Be sure to keep original copies of all files you plan to modify**! It can be cumbersome--and expensive--to re-extract the entire game if you fail to heed this disclaimer. You've been warned! 

## Texture Replacements
To make a texture replacement, we will need to find to the model's source texture. For this example we will replace Sora (DDD)'s base texture.

#### 3DS
1. Using Exam Editor, navigate to the `Nightmare Editor` option. This will bring up a new screen.
2. Ensure **chara_pc.rbin** has already been unpacked. **Select chara_pc.rbin** and filter on Model files (*.pmo) and search for **p_ex010.pmo**.
3. Right-click on `p_ex010_01.ctt > Open Folder`. This will open the folder in your file explorer. 

![Image](<img/nem2.png>)

4. Edit your texture to your heart's content, in your favorite picture editor! 
    * Generally, every texture will be saved without transparency, so keep that in mind.
    * Textures will also need to be the same dimensions as the original file. Ignoring this will cause your texture to display incorrectly in-game, or even crash your game.
5. To pack your texture file, navigate to your model file and click on `Link New Texture`. This will open a file explorer window. Navigate to your edited texture file.
6. Right click on the texture filename (ie. **p_ex010_01.ctt**), and queue the file. This is necessary to repack the game files.
7. Repeat for additional edits for other models or textures.
8. After completing all texture edits, click on the `View Files` button. This will bring up all of the files you have queued. Verify all of your edits have been queued. Once you are ready, click on Export Mod. 

![Image](<img/nem3.png>)

9. This brings up a new `Create Mod` window. Add in details where appropriate. Click Confirm once you're done.

![Image](<img/nem4.png>)

10. Save your mod file. You can navigate back to Exam Editor to install your mod!

#### PC
1. Navigate to Mod Manager's `extract` folder. Texture files are located in `\remastered`. For this example we will navigate to:
 `[..]\remastered\chara\pc\p_ex01\mig\0\bin\p_ex010.pmo\`. 

![Image](<img/tex1.png>)

2. _**Copy**_ the files you want to edit to your working folder, and edit your texture to your heart's content! 
    * Directly modifying the file WILL modify the texture in-game, but if there's ever a need to restore this texture you will need to re-extract the game. A very expensive mistake! 
3. In your working folder, structure your folders and files in a way that makes sense to you. A typical case is to replicate the folder structure as the original file (ie. `[..]\remastered\chara\pc\p_ex01\mig\0\bin\p_ex010.pmo\`.)
4. Build your mod.yml. This can be done manually or with Mod Manager. Here's an example:
```
title: Sora - Recolor
originalAuthor: <your username>
description: Recolor of Sora.
assets:
  - name: remastered\chara\pc\p_ex01\mig\0\bin\p_ex010.pmo\p_ex010_01.dds
    method: copy
    source:
      - name: remastered\chara_pc\p_ex010\p_ex010_01.dds
```
5. If you did everything right, your mod should show up in the list of mods for Dream Drop Distance! Build and run to enjoy your texture replacement.


## Model Replacements
Model replacements will take a lot more elbow grease. As long as you have a valid 3D model that can be exported as FBX, you can replace the target model with just about any source model. This section will assume you have basic knowledge of Blender or related 3D-modeling software, and you have already extracted game files for related _KINGDOM HEARTS_ games. 

We will first focus on acquiring our target model (the model we will be replacing). 

### Converting _Dream Drop Distance_'s PMO to FBX
As of writing, PMO files are view-only and can only be converted with the appropriate tools. 
1. Navigate to the file you want to replace. We will use **p_ex020.pmo** for this example.
2. Open **OpenKH.KhModels**, then drag-drop your PMO. 
3. Under `File > Export`, and save your model into your working folder.

![Image](<img/khm1.png>)

I will now go over acquiring a model from other _KINGDOM HEARTS_ games. Skip ahead if this step is not relevant to you. 

### Converting _Birth By Sleep_'s PMO to FBX
_Dream Drop Distance_ and _Birth By Sleep_ share a filetype, but have different data in their header, meaning they are not yet compatible with our game. _Birth By Sleep_ famously keeps all files within an ARC file, which we will need to unpack before we get to our PMO. We can do this one of two ways:
1. **OpenKh.Command.Arc.exe**:
    1. Prepare an `unpacked` folder for the ARC files to be exported to. 
    2. Open **Powershell** within OpenKH's root directory ("Shift + right click > Open Powershell window here"). 
    3. Enter the following:
    `.\Apps\OpenKh.Command.Arc.exe <location of ARC file> <location of your "unpacked" folder>`

![Image](<img/arc1.png>)

    4. In **OpenKH.KhModels**, drag-drop the newly generated PMO. Go to `File > Export` and save your exported FBX in your working folder.
2. **KHBBSMesh**:
    1. Open **KHBBSMesh**, then drag-drop the ARC file. A list window will pop up. 
    2. Load the PMO, then go to `File > Export`
    3. After configuring your export options, export the file as FBX. 

![Image](<img/anm1.png>)

Alternatively, a PMO from _Birth By Sleep_ can be directly converted to be used in _Dream Drop Distance_ by using Kite98's **PMO Builder** or **KH Asset Studio**. 
1. Open either program, then drag-drop the PMO.
2. Save the PMO as a _Dream Drop Distance_ model object. 

### Converting MDLX to FBX
_KINGDOM HEARTS II_ uses MDLX, which is well documented at this point. I have had the most success exporting FBXs with the following method.
1. Open **OpenKh.MdlxEditor**, and drag-drop your MDLX.
2. Under ``File > Export model > FBX``, save your model into your working folder. 

![Image](<img/khm2.png>)


### Replacing the Target Model
1. Open **Blender** and import your target FBX. Voila! You now have... a very tiny model and armature. Zoom in a bit and verify your armature, meshes, and textures look as expected.
    * There can be multiple meshes for a single armature. It is usually better to leave these alone (they may have varying weights or UV mapping that may merge or be destroyed).
2. Import the source FBX. Edit the mesh so it matches the same size, pose, and placement as the target mesh.
    * It is very important you do NOT modify the original armature. If your source mesh came with its own armature; 
        1. Pose your model
        2. Duplicate the Deform Armature modifier
        3. Ctrl + A to set the rest pose
        4. Apply one of the Deform Armature modifiers

![Image](<img/mdl1.png>)

3. Parent your _source mesh_ to the _target armature_, with empty vertex groups. 
    1. Change the transform pivot point to 3D Cursor (assuming it is at position 0, 0, 0).
    2. In Edit Mode, edit your _source mesh_ to match the position of your _target armature_. You may need to scale the mesh by increments of 100x or 0.01x. 
    3. In Object Mode, reset the rotation, location, and scale of the _target armature_ (Alt + R, Alt + G, Alt + S). The armature will most likely rotate 90 degrees clockwise along the Y-axis.
    4. In Edit Mode, edit your _source mesh_ to match the new rotation. 
    5. Now, in Object Mode parent your _source mesh_ to the _target armature_ (Ctrl + P), with "Empty Vertex Groups".
        * This is done by selecting the mesh __first__, then the armature __second__. 
    6. Rotate the _target armature_ 90 degrees counter-clockwise.
4. Weight paint your model to the new vertex groups. This can be done by:
    * Weight mixing (`Modifiers tab > Vertex Weight Mixing`)
    * Copying existing vertex groups
    * Manual weight painting
    * (Try your luck with) automatic weight painting

![Image](<img/mdl2.png>)

5. Reference your textures into your model. 
    * By default, if they are in the same working folder as the FBX you imported, Blender will reference them automatically.
    * Limit your textures to a max size of 512 x 512 px, as the game engine may not know how to properly handle anything larger than that.
6. Rename the mesh to your model name. This is to prevent your model from appearing where they're not supposed to (like "cutscene ghosting"... spooky!).

![Image](<img/mdl3.png>)

7. Finally, export your FBX. Ensure you are exporting your new model! Exporting grabs *everything* in the .blend file, so remove anything you're not planning on exporting. While exporting, review these changes as well:
    * Remove "Add Leaf Bones"

### Packing the New PMO
Congratulations on your new FBX! Open Kite98's PMO Builder, then locate your new FBX. Select "PMOs for _Dream Drop Distance_", and select texture encoding types. 
* **RGB565**: a general-use best-compatability image encoding type(necessary for eye/mouth meshes)
* **ETC1**: high-quality image compression (no transparency)
* **ETC1A4**: alpha-enabled image compression (includes transparency)
If everything went well, you can drag-drop your new PMO into either KHModels or KHBBSMesh to preview your work. If all looks good, you can structure your mod folder for OpenKH or Nightmare Editor.

#### 3DS
1. Using Exam Editor, navigate to the ``Nightmare Editor`` option. This will bring up a new screen.
2. Ensure the relevant **.rbin** has already been unpacked. Filter and search for your PMO.
3. Right-click on your **PMO**, and queue the file. This is necessary to repack the game files.
4. Repeat for any other models.
5. After queueing all your model replacements, click on the ``View Files`` button. This will bring up all of the files you have queued. Verify all of your models have been queued. Once you are ready, click on ``Export Mod``.
6. This brings up a new ``Create Mod`` window. Add in details where appropriate. Click ``Confirm`` once you are done. 
    * This is to create the folder structure for our mod. We will be replacing these PMOs with our newly created ones.
7. Save your mod file, then navigate back to Exam Editor.
8. Find your mod within Nightmare Editor's list, then ``right click > Open Mod Folder``. Replace the PMOs in this folder with your newly created ones.
9. Deploy the mod to enjoy your new model replacement!

#### PC
1. In your working folder, structure your folders and files in a way that makes sense to you. A typical case is to replicate the folder structure as the original file (ie. `[..]\chara\pc\p_ex01\mig\0\bin\`).
2. Build your `mod.yml`. This can be done manually or with Mod Manager. Here's an example:
```
title: Keyblade - Delta Weapon
originalAuthor: <your username>
description: Replacing Kingdom Key with another model. 
assets:
  - name: chara/wep/w_so01/mig/0/bin/w_so010.pmo
    method: copy
    source:
      - name: 3ds/chara_wep/10-w_so010.pmo
```
3. If you did everything right, your mod should show up in the list of mods for Dream Drop Distance! Build and run to enjoy your model replacement.

## Animation Replacements
If you are feeling extra passionate about this game, animation replacements are also possible thanks to the many contributions done by dedicated researchers and developers. 

### Disclaimers and Limitations
If you are merely swapping a handful of animations for a model, you will need to keep the original model's armature. However, if you are making a full model + animation replacement you do not need to adhere to the original armature; you can simply use your new model's armature. However, any armature will, at minimum, need `Root`, `center`, `L/R_ashi2` (for feet positioning), and `L/R_buki` (for weapon positioning) bones.

In my experience, a full character replacement (with a new armature) is possible if you replace ALL animations relating to that model--including cutscenes. Animation data will expect the related model to have the correct bone indexes (AKA bone name + bone order). So, if there is an animation you do not replace, the game will try to continue by T-posing... but will more commonly just crash the game. This is true for both 3DS and PC versions. I have gotten around this by replacing all cutscene models with an idle animation. 

Conversely, reusing the original model's armature poses its own set of challenges. _Dream Drop Distance_ allows multi-weight grouping, meaning you can be creative about multiple bones influencing a single weight group. However, any animations you do not replace will shrink or stretch your model unexpectedly, and in my experience making too many sacrifices to squeeze a model into a different armature can be frustrating. 

Having done both, I lean towards a FULL character replacement, as it gives total control of the armature despite the extra work that comes with it. Regardless of my opinion, pick a design philosophy and stick with it!

Most animations do not need to follow the same frame count as the original, especially ones that loop. However, there may be a command or base animation that relies on the exact frame count (ie. Balloonra needs Animation 317 and 318 to be EXACTLY 34 and 33 frames, respectively). In these cases be sure to adjust your animation to match the original frame count. 

Lastly... any project, including one of this scope, is a marathon and not a sprint. Work incrementally--once you have a handful of animations done, I encourage you to cobble them together and test them in-game. Do not be disheartened if something does not look right. Take note of it, fix where you can, maybe take a break, then move onto the next one.

That being said... if you are ready, we can get started!

### Prerequisites
* A retargetting plugin of choice (Rokoko, Auto Rig Pro, etc)
* A source model (with the animation you want to retarget)
* A target model (the model you want to put your animation on)

### Gathering _Dream Drop Distance_/_Birth By Sleep_ Animations
In both games, animations are indexed as XXX. Each game references the animation index for each command, action, and reaction. Both games share indexes for most actions, which is helpful if you are looking for an equivalent _Dream Drop Distance_ animation for a _Birth By Sleep_ character and vice versa (like casting Thunder magic).

1. Using **KHBBSMesh**, drag-drop either an ARC file or BBS-version PMO
    * If importing an ARC file, there will be a menu to import a PMO and PAM.
    * If importing a PMO from _Birth By Sleep_, drag-drop the corresponding PAM file.
    * If Importing a PMO from _Dream Drop Distance_, first convert using Kite's PMO Builder to a _Birth By Sleep_ version, then import into KHBBSMesh. 
    * Similarly, convert a _Dream Drop Distance_ PAM to a _Birth By Sleep_ version, then import into KHBBSMesh. 
2. Under the `Skeleton` menu select which animation to play.
3. Under `File > Export`, select the animation you want to export.
    * By default, exported animations will be located in `.\resources\export`. I recommend exporting as `Autodesk FBX (ascii)`.

![Image](<img/anm1.png>)

4. Repeat for any additional animations. 


### Gathering _KINGDOM HEARTS 2_ Animations
1. Using **KH2MsetMotionEditor**, import a matching set of MDLX and MSET files.
2. Under `MotionPlayer` select which animation to play/extract.
3. Under `File > Export current motion to FBX`, save your animation to your working folder.

![Image](<img/khm3.png>)

4. Repeat for any additional animations.

### Importing Animations for Retargetting 
1. Import your target model, then your source model.
2. Navigate to the Rokoko (or equivalent retarget plugin) menu. Set your source and target models. 

![Image](<img/anm2.png>)

3. Verify your two models' rest (or current) poses are generally aligned, then click Build Bone List. Adjust any settings as necessary.
    * This will generate a list of bones and what Rokoko thinks is its corresponding bone to retarget. Only one source bone can be retargetted to one target bone at a time. 
    * You can also try `Auto-Scale`, which will mainly copy the rotations of your source animation to your target armature. 
    * Remove `Root` and `center` from your retargetting. Keeping them in often messes with the vertical or horizontal movement and will cause your animation to look stiff. If the animation needs both bones, you can:
        1. Copy the keyframes from the source animation's animation timeline _after_ retargetting
        2. Keyframe them yourself
4. Click `Retarget Animation`. If all goes well, your animation should now be on your target armature!
    * This will take some trial and error. If something looks awry, test your animation, and adjust bone list settings as needed. 
    * Retargetting isn't perfect. Child bones usually only copy rotations, so you can keyframe a new location for any incorrectly placed bone.
    * Graph Editor can be helpful in adjusting translation speeds (Using Linear vs Bezier)
    * _Dream Drop Distance_ calculates animations as 30fps, so create each animation with that restriction in mind 
        * (ie. a 72-frame animation in 60fps will calculate as 36-frames in 30fps within _Dream Drop Distance_'s engine). 
5. Keyframe any bones not retargetted. I usually just put a single keyframe at frame 1 for bones without any keyframes post-retarget.
6. In the Output Properties, adjust the `Frame Range` to the length of the animation + 1 frame. In the animation timeline, move the final keyframe to the new endpoint.
    * Animation inserts, at some point, lose the last keyframe. Adding in a dummy keyframe ensures each animation ends as intended. 
7. Export your animation as an FBX. I like to keep the following settings on:
    * Remove `Add Leaf Bones`
    * Remove `NLA Strips`
    * Remove `All Actions`
    * `(Optional)` Add `Key All Bones`

![Image](<img/mdl4.png>)

8. Repeat for any addtional new animations. Don't forget to save all of your .blend files!

### Packing the Animations into a PAM
Once you have your collection of animations, find your model's PAM files. There may be as few as 2, or as many as 170 files. Hang in there!

![Image](<img/anm4.png>)

1. Drag-drop each PAM into PAM Editor, then click on `PAM Maker`. We will import each of our animations into our model's PAM.
    * You may need to resize the animation for the game engine. In most cases you can scale by 100x or 0.01x. 
    * Most animations do not need interpolation, but basic movement (like idling, walking/running, or hurt animations) will need 8 to 12 frames of interpolation. 
    * Set `Custom Loop Points` for dashes and rolls to 0. Looping the animation will reset the player movement, causing some rubberband movement in-game. 
    * For most cases I recommend leaving `Reset root-bone translation & rotation` off.
2. For best practice, make sure the `Flag` matches the original. Although it is currently unknown what this does, we want to make sure our character works as expected in-game. 

![Image](<img/anm3.png>)

3. Repeat this process for all animations across all PAM files. 
    * If there are some repeat animations you may also `Right click > Extract Animation` for any of them, and import into another. Each PAMANIM will retain interpolation and loop information. 

Once you have all of your PAMs in order, we can get these ready for the game.

#### 3DS
1. Using Exam Editor, navigate to the ``Nightmare Editor`` option. This will bring up a new screen.
2. Ensure the relevant **.rbin** has already been unpacked. Filter and search for your **PAM**.
3. Right-click on your **PAM**, and queue the file. This is necessary to repack the game files.
4. Repeat for any other models.
5. After queueing all your model replacements, click on the ``View Files`` button. This will bring up all of the files you have queued. Verify all of your models have been queued. Once you are ready, click on ``Export Mod``.
6. This brings up a new ``Create Mod`` window. Add in details where appropriate. Click ``Confirm`` once you are done. 
    * This is to create the folder structure for our mod. We will be  adding our PAMs afterwards.
7. Save your mod file, then navigate back to Exam Editor.
8. Find your mod within Nightmare Editor's list, then ``right click > Open Mod Folder``. Replace and/or add your PAMs (and PMOs, if you have any) in this folder with your newly created ones.
9. Deploy the mod to enjoy your new character replacement!

#### PC
1. In your working folder, structure your folders and files in a way that makes sense to you. A typical case is to replicate the folder structure as the original file (ie. `[..]\chara\pc\p_ex01\mig\0\bin\`).
2. Build your `mod.yml`. This can be done manually or with Mod Manager. Here's an example:
```
title: Riku - New Animations
originalAuthor: <your username>
description: Riku with a new coat. Includes new animations. 
assets:
## Player Model
  - name: chara\pc\p_ex02\mig\0\bin\p_ex020.pmo
    method: copy
    source:
      - name: 3ds\chara_pc\1-p_ex020.pmo
      
## Animations
  - name: chara\pc\p_ex02\anm\rt\bin\p_ex02_001.pam
    method: copy
    source:
      - name: 3ds\chara_pc\57-p_ex02_001.pam
```
3. If you did everything right, your mod should show up in the list of mods for Dream Drop Distance! Build and run to enjoy your character replacement!

## Closing
I hope this was useful! If you have any questions, reach out to the kind folks on the OpenKH server. Good luck on your modding endeavors!
