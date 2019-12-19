# godot_3.1_gameshell

Export templates for Godot Engine v 3.1.2 stable built on ClockworkPi Gameshell firmware 0.4

How to use these templates to export your Godot project to be a playable game on ClockworkPi Gameshell:
1. Run Git Clone on the machine you are developing your game in Godot
`git clone https://github.com/apyoungblood/godot_3.1_cpi.git`
2. Unzip the export templates
3. Install Clockworkpi GameShell Firmware Current Version 0.4 [Download ClockworkOS for GameShell version 0.4](https://forum.clockworkpi.com/t/gameshell-os-image-files-v0-4-latest/355) use [Etcher](https://www.balena.io/etcher/) to write the extracted firmware to your device's microSD card *This will wipe your device, so backup any files you want beforehand* Or dd and pv on linux shell `pv firmware-file-name.img | sudo dd of=/dev/mmcblk#` where mmcblk# is your SD Card, if you want to find it I suggest the `lsblk` command. 
  > I like to use HPCodecraft's script for setting up my device after flashing a fresh firmware image on it to do so run `wget https://raw.githubusercontent.com/hpcodecraft/gameshell-setup/master/run.sh` then `./run.sh`
4. Make your game in Godot Engine Version 3.1.2 stable, on any OS (Windows, Linux, MacOS)

  > Considerations: Make sure to set the Project Settings > Display > Window to 320 width and 240 height, as that's the resolution of the GameShell and you'll get crashes/errors if you use anything else.
  > It's always a good idea to give yourself a way to quit the game when you are done playing. In Godot we can add this script (assuming you've mapped ui_escape to the Escape key on the keyboard in Project Settings):
  ```python
  if Input.is_action_pressed("ui_escape")
    get_tree().quit()
  ```
5. Godot project binaries can be built from any OS in Godot 3.1.2 stable using the following settings:
![Godot Project Settings](https://sjc2.discourse-cdn.com/standard17/uploads/clockworkpi/optimized/2X/4/41475fa1c9c3f7b58979d16562e3ae854843ba1e_2_477x375.png)
_Under Custom Template use the binaries I’ve built and posted to the github url below. Be sure 64 bits is NOT selected under Binary Format_
6. Add the following line to the end of your GameShell's .bashrc file, which should be in /home/cpi/.bashrc `export DISPLAY=:0` then reboot your GameShell
7. Copy the exported file from earlier (should be ProjectName.x86 in the Bin directory of you Godot Project Folder as well as the .pck file) to your GameShell in a directory where you want it.I suggest /home/cpi/games/ProjectName/ProjectName.x86
8. Change to that directory and change the privlieges on those files:

  `cd ~/games/ProjectName/`
  
  `chmod +x *`
  
9. Create a launcher entry:

  `cd ~/launcher/Menu/GameShell`
  
  `vi 21_ProjectName.sh` This can be any name, and the number is not required, but must be different than anything already in this directory which you can see with the `ls` command, additionally you can use nano or your text editor of choice instead of vim
  
  Add the following to the file and save it:
  
  `#!/bin/bash`
  
  `exec /home/cpi/games/ProjectName/ProjectName.x86` _where ProjectName is whatever you've named your game_
  
  Finally, we need to make sure that this new script is executable:
  
  `chmod +x 21_ProjectName.sh`

10. Reload the UI on your GameShell. That's it! Select your game and play!  

## Process for creating export templates

Compiled on ClockworkPi Gameshell using the following command:

`scons platform=x11 -j6 use_llvm=yes tools=no target=release bits=32 &`

I tried this on the GameShell without the use_llvm=yes parameter which as yes uses clang and without uses gcc, but the gcc compiler fails with errors. I added the -j6 parameter which is recommended by Godot which runs 6 jobs and they recommend cpu cores + 1 to 2, since the GameShell has 4, I tried 6.

_\*This process took about 2 hours to run on device_

## Known Issues

The sound driver logs to the terminal "under-run" errors with the ALSA sound driver.

```
cpi@clockworkpi:~/Platformer$ ./Platformer_2D.x86
OpenGL ES 2.0 Renderer: Gallium 0.4 on llvmpipe (LLVM 3.9, 128 bits)
ALSA lib pcm.c:8306:(snd_pcm_recover) underrun occurred
```
Currently this is only supported for the fbturbo software display drivers as the lima drivers are not fully functional and stable yet. There's a post on the CPi forums that indicates a successfull use of my previous version of export templates and the custom DEOT v1 image, though I've been unsuccessful in my testing of that. If anyone tries that and gets a game to work, please let me know as the custom DEOT v1 image should have updated lima and mesa drivers and would likely run any game faster and better.
