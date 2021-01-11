# VLC 3.0 Lua Extension Guide
This a documentation for writing extensions in lua for vlc 3, as parts of the [lua readme](https://www.videolan.org/developers/vlc/share/lua/README.txt) provided by Video Lan is depcricated. So I made this guide to supplement the readme, for any questions and confusion others may have

to download the source code for VLC-3.0 visit the [git lab page](https://code.videolan.org/videolan/vlc-3.0)
callback functions that you use to communicate to VLC:
- descriptor
- activate()
- deactivate()
- close()
- input_changed()
- playing_changed()
- meta_changed()
- menu()
- trigger_menu(id)

read more in detail about these functions here [template-plugin.lua](https://github.com/nima64/vlc-lua-extension-template/blob/main/template-plugin.lua)  
The minumim vlc requires for extension to work is a descriptor(needed to show up in menu) and activate.
**custom callbacks through add_callback() is depericated, so you cannot add functions to the event loop. Creating your event loop is possible,but you'll have to do it through a vlc interface which communicates to your extension, see the Time extension and interface in videolan's adddon page to learn more**  
  
For debugging run vlc with the verbose argument v ex: vlc -v  
In vlc 3 the player object is deprecated, so to get the current media object use input instead.  

## Getting and Changing the current media data  ##
manipulating the player can be done through the vlc.var command
vlc.var.get(vlc.object.input(),"time") --vlc time is ms(microseconds) or in seconds = ms*10^-6 
vlc.var.set(vlc.object.input(),"time",3243)
vlc.var.set(vlc.object.input(),"time-offset",-300) --offsed +- current time
vlc.var.get(vlc.object.input(),"position")
vlc.var.set(vlc.object.input(),"position",3240)
## URI file handling in VLC ##  
vlc paths are all handled in URI,
to create a uri a path, use vlc.strings.make_uri(path)
ex output: win file:///C:/User/bob/Desktop/man%20eating%20burger.mp4
unix/linux file:///home/bob/Desktop/man%20eating%20burger.mp4  
NOTE: when parsing for path with windows you need to remove file:/// 3 forward slashes,  while with unix/linux you need to remove 2 file://.  

when calling make_uri in windows,vlc requires the slashes to be back slashes '\' foward slashes will be redirected to vlc's config directory.  
ex: vlc.strings.make_uri("C:\User\bob\Desktop\man eating burger.mp4") -> outputs see win uri example  

## VLC api calls ##
VLC Objects acessible via vlc.object (modules/lua/object.c):
- input
- playlist
- libvlc
- find
- vout
- aout  

VLC Sub Modules (modules/lua/extension.c):
- config()
- dialog()
- input()
- msg()
- object()
- osd()
- playlist()
- stream()
- strings()
- variables()
- video()
- vlm()
- volume()
- xml()
- vlcio()
- errno()
- rand()
- rd()
- gettext()
- equalizer()

vlc.input methods:
- is_playing()
- item() -> returns an item obj
- add_subtitle()
- add_subtitle_mrl()

item obj methods
- is_preparsed
- metas
- set_meta
- uri
- name
- duration
- stats
- info

vlc.var methods:
- inherit()
- get()
- get_list()
- set()
- create()
- trigger_callback()
- libvlc_command()
- inc_integer()
- dec_integer()
- count_choices()
- toggle_bool()

Valid String Argument for Var(inputObject,arg):
- state
- rate
- position
- time
- time-offset
- bookmark
- program
- title
- chapter
- audio-delay
- spu-delay
- video-es
- audio-es
- spu-es
- record
- frame-next





