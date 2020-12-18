# VLC-3 Lua Extension Guide
This a documentation for writing extensions in lua for vlc 3, as the current docs online is deprecated for 3.0.

to download the source code for VLC-3.0 visit the [git lab page](https://code.videolan.org/videolan/vlc-3.0)
## Making a barebones hello world window/dialog

callback functions that you use to communicate to VLC:
- descriptor (sends meta data about your plugin)
- activate()
- deactivate()
- close()
- input_changed()
- playing_changed()
- meta_changed()
- menu()
- trigger_menu(id)  
to see more details regarding these functions see [template-plugin.lua](https://github.com/nima64/vlc-lua-extension-template/blob/main/template-plugin.lua)

```lua
function descriptor()
	return {
		title = "VLC Extension - Basic structure",
		version = "1.0",
		author = "",
		url = 'http://',
		shortdesc = "short description",
		description = "full description",
		capabilities = {"menu", "input-listener", "meta-listener", "playing-listener"}
	}
end
function activate()
  createDialog()
end
function close()
	vlc.deactivate()
end
function createDialog()
	local d = vlc.dialog("helloworld extension")
  --add_label(txt,col,row,col_span,row_span)
	d:add_label("helloworld",1,1,1,1)
end
```
The Descriptor is required for your plugin to appear in the menu.
To create the gui we have to acess the VLC api, which is acessed through the global **vlc** object.  
Make a dialog through vlc.dialog(title), then we added a label inorder for something to show
add_label("helloworld",1,1,1,1)  
For debugging use run vlc with a -v ex: vlc -v
To readmore see https://www.videolan.org/developers/vlc/share/lua/README.txt, **Disclaimer parts of it are depericated for VLC-3.0**  


VLC Objects via vlc.object (modules/lua/object.c):
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

## Sub-Module Methods

VLC Input:
- is_playing()
- item()
- add_subtitle()
- add_subtitle_mrl()

VLC InputItem via vlc.iput.item() (input.c)
- is_preparsed
- metas
- set_meta
- uri
- name
- duration
- stats
- info

VLC Var methods:
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





