# VLC 3.0 Lua Extension Guide
This a documentation for writing extensions in lua for vlc 3, as parts of the [lua readme](https://www.videolan.org/developers/vlc/share/lua/README.txt) provided by Video Lan is deprecated. So I made this guide to supplement the readme for any questions and confusion others may have.

to download the source code for VLC-3.0 visit the [git lab page](https://code.videolan.org/videolan/vlc-3.0)  
callback functions that you use to communicate to VLC:  
*activate  
deactivate  
input_changed  
playing_changed  
meta_changed  
trigger_menu(id)*

read more in detail about these functions here template-plugin.lua

The minumim vlc requires for extension to work is descriptor (needed to show up in menu) and activate funcitons.  

*Custom callbacks through add_callback() is deprecated, so you cannot add functions to the event loop. Creating your event loop is possible,but you'll have to do it through a vlc interface which will communicate to your extension. See the "Time extension and interface" in videolan's adddon page to learn more*  
  
For debugging run vlc with the verbose argument v ex: vlc -v  
In vlc 3 the player object is deprecated, so to get the current media object use input instead.  

### Getting and Changing the current media data  ###
manipulating the player can be done through the **vlc.var**  

vlc.var.get(vlc.object.input(),"time") returns in microseconds,for seconds use ms*10^-6  

vlc.var.set(vlc.object.input(),"time",3243)
vlc.var.set(vlc.object.input(),"time-offset",-300)  
vlc.var.get(vlc.object.input(),"position")  
vlc.var.set(vlc.object.input(),"position",3240)  

### URI file handling in VLC ###  
vlc paths are all handled in URI  
to create a uri path use vlc.strings.make_uri(path).

In windows use backslashes \ in your path, if you use / foward slashes your path will be appended to vlc's config directory.  

Example of a correct path:  
vlc.strings.make_uri("C:\User\bob\Desktop\man eating burger.mp4") 

make_uri output:  
win "file:///C:/User/bob/Desktop/man%20eating%20burger.mp4"  
unix/linux "file:///home/bob/Desktop/man%20eating%20burger.mp4"  

NOTE: when parsing for a path with windows you need to remove "file:///" 3 forward slashes.
While with unix/linux you need to remove 2, "file://"  


### Reference ###
| VLC Objects acessible via vlc.object (modules/lua/object.c) |
| ---                                                         |
| input |
| playlist |
| libvlc |
| find |
| vout |
| aout  |

|VLC Sub Modules (modules/lua/extension.c):|
|---|
| config()|
| dialog()|
| input()|
| msg()|
| object()|
| osd()|
| playlist()|
| stream()|
| strings()|
| variables()|
| video()|
| vlm()|
| volume()|
| xml()|
| vlcio()|
| errno()|
| rand()|
| rd()|
| gettext()|
| equalizer()|

|vlc.input methods:|
|---|
| is_playing()|
| item() -> returns an item obj|
| add_subtitle()|
| add_subtitle_mrl()|

|item obj methods|
|---|
| is_preparsed|
| metas|
| set_meta|
| uri|
| name|
| duration|
| stats|
| info|

|vlc.var methods:|
|---|
| inherit()|
| get()|
| get_list()|
| set()|
| create()|
| trigger_callback()|
| libvlc_command()|
| inc_integer()|
| dec_integer()|
| count_choices()|
| toggle_bool()|

|Valid String Argument for Var(inputObject,arg):|
|---|
| state|
| rate|
| position|
| time|
| time-offset|
| bookmark|
| program|
| title|
| chapter|
| audio-delay|
| spu-delay|
| video-es|
| audio-es|
| spu-es|
| record|
| frame-next|





