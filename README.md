# godot_3.1_gameshell

An export template for Godot Engine v 3.1 stable built on ClockworkPi Gameshell

Compiled on ClockworkPi Gameshell using the following command:

`scons platform=x11 -j6 use_llvm=yes tools=no target=release bits=32 &`

I tried this on the GameShell without the use_llvm=yes parameter which as yes uses clang and without uses gcc, but the gcc compiler fails with errors. I added the -j6 parameter which is recommended by Godot which runs 6 jobs and they recommend cpu cores + 1 to 2, since the GameShell has 4, I tried 6.

_\*This process took about 2 hours to run on device_

## Update from GameShell ClockworkOS v0.21

For grins I tried going back to the ClockworkOS v0.21 from v0.3 (installed on my main SD card that shipped with my GameShell). I have an extra 8GB SD card with 0.21 for testing and such. This actually ran the game fine. This feels like more validation to me that the problem is with the Lima driver than anything else, though I thought I'd tried it with the driver switched to fbturbo in firmware 0.3. It's also important to acknowledge what I believe to be a separate issue with the sound driver in this case errors as "under-run" and on v0.3 firmware gives a "over-run" error with the ALSA sound driver.

```
cpi@clockworkpi:~/Platformer$ ./Platformer_2D.x86
OpenGL ES 2.0 Renderer: Gallium 0.4 on llvmpipe (LLVM 3.9, 128 bits)
ALSA lib pcm.c:8306:(snd_pcm_recover) underrun occurred
```

Running the exported project binaries with debugging gave the following errors along with distorted but playing sound and input that worked, but no visuals following the Godot Engine splash screen:

```
cpi@clockworkpi:~/downloads/godot_3.1/platformer2d$ ./Platformer_2D.x86 --video-driver GLES2 --verbose
XInput: Refreshing devices.
XInput: No touch devices found.
Detecting GPUs, set DRI_PRIME in the environment to override GPU detection logic.
X Error of failed request:  GLXBadFBConfig
  Major opcode of failed request:  155 (GLX)
  Minor opcode of failed request:  34 ()
  Serial number of failed request:  25
  Current serial number in output stream:  22
X Error of failed request:  GLXBadFBConfig
  Major opcode of failed request:  155 (GLX)
  Minor opcode of failed request:  34 ()
  Serial number of failed request:  25
  Current serial number in output stream:  22
Only one GPU found, using default.
XcursorGetTheme could not get cursor theme
Using GLES2 video driver
OpenGL ES 2.0 Renderer: Mali400
error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_OPERATION in glTexImage2D(bad target for texture)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
ERROR: initialize: Directional shadow framebuffer status invalid
   At: drivers/gles2/rasterizer_scene_gles2.cpp:3355.
Audio buffer frames: 512 calculated latency: 11ms
error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

error: lima_blit not implemented

CORE API HASH: 0
EDITOR API HASH: 0
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_FRAMEBUFFER_OPERATION in glClear(incomplete framebuffer)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
WARNING: _render_target_allocate: Could not create framebuffer!!
   At: drivers/gles2/rasterizer_storage_gles2.cpp:4605.
ERROR: _gl_debug_print: GL ERROR: Source: OpenGL        Type: Error     ID: 2   Severity: High  Message: GL_INVALID_FRAMEBUFFER_OPERATION in glClear(incomplete framebuffer)
   At: drivers/gles2/rasterizer_gles2.cpp:134.
Loading resource: res://Stage.tscn
Loading resource: res://TileSet.tres
Loading resource: res://tiles_demo.png
Loading resource: res://coin/Coin.tscn
Loading resource: res://coin/coin.gdc
Loading resource: res://player/player.gdc
Loading resource: res://player/Bullet.tscn
Loading resource: res://player/bullet.gdc
Loading resource: res://player/bullet.png
Loading resource: res://coin/coin.png
Loading resource: res://audio/sound_coin.wav
Loading resource: res://platform/MovingPlatform.tscn
Loading resource: res://platform/moving_platform.gdc
Loading resource: res://platform/moving_platform.png
Loading resource: res://platform/OneWayPlatform.tscn
Loading resource: res://platform/one_way_platform.png
Loading resource: res://player/Player.tscn
Loading resource: res://player/robot_demo.png
Loading resource: res://audio/sound_jump.wav
Loading resource: res://audio/sound_shoot.wav
Loading resource: res://player/osb_left.png
Loading resource: res://player/osb_right.png
Loading resource: res://player/osb_jump.png
Loading resource: res://player/osb_fire.png
Loading resource: res://enemy/Enemy.tscn
Loading resource: res://enemy/enemy.gdc
Loading resource: res://enemy/enemy.png
Loading resource: res://audio/sound_hit.wav
Loading resource: res://audio/sound_explode.wav
Loading resource: res://background/ParallaxBg.tscn
Loading resource: res://background/scroll_bg_sky.png
Loading resource: res://background/scroll_bg_cloud_1.png
Loading resource: res://background/scroll_bg_cloud_2.png
Loading resource: res://background/scroll_bg_cloud_3.png
Loading resource: res://background/scroll_bg_fg_2.png
Loading resource: res://background/scroll_bg_fg_1.png
Loading resource: res://audio/music.ogg
ALSA lib pcm.c:8306:(snd_pcm_recover) underrun occurred
```
