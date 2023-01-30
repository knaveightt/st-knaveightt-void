# st-knaveightt-void (st-0.9)
> Patch used to modify the [st terminal](https://st.suckless.org) used for my
> workstations. This patch is provided against st-0.9 for use with xbps-src to
> automate patching and installation in void linux.

## Usage 
Included in this repo is a patch file which represents a collection of patches
to the original st source. The following are usage instructions for
incorporating this patch using Void Linux's xbps-src build workflow, however
the final patch can be used any way you would normally patch st. 
- Copy the patch file to a *patches* directory in `void-packages/srcpkgs/st` 
- Run `xbps-src pkg st` to build the xbps package
- Install the package from the void-packages directory using `sudo xbps-install
  --force --repository=hostdir/binpkgs/ st`
- Recommendation is to lock the st package to the local repo so changes from
  the default repositories don't overwrite the package. Do this using
  `xbps-pkgdb -m repolock st`

## Patch List
List of included patches are as follows.
| Patch Name | Source URL |
| ---------- | ---------- |
| glyph wide support | [https://st.suckless.org/patches/glyph_wide_support/st-glyph-wide-support-20220411-ef05519.diff](https://st.suckless.org/patches/glyph_wide_support/st-glyph-wide-support-20220411-ef05519.diff) | 
| xresources | [https://st.suckless.org/patches/xresources/st-xresources-20200604-9ba7ecf.diff](https://st.suckless.org/patches/xresources/st-xresources-20200604-9ba7ecf.diff) |
| defaultfontsize | [https://st.suckless.org/patches/defaultfontsize/st-defaultfontsize-20210225-4ef0cbd.diff](https://st.suckless.org/patches/defaultfontsize/st-defaultfontsize-20210225-4ef0cbd.diff) |
| anysize | [https://st.suckless.org/patches/anysize/st-anysize-20220718-baa9357.diff](https://st.suckless.org/patches/anysize/st-anysize-20220718-baa9357.diff) |
| font2   | [https://st.suckless.org/patches/font2/st-font2-0.8.5.diff](https://st.suckless.org/patches/font2/st-font2-0.8.5.diff) |
| scrollback | [https://st.suckless.org/patches/scrollback/](https://st.suckless.org/patches/scrollback/)

## Patch Application and Modifications
Below is a breakdown of how I patched my instance of st. I've also included a
script called *create_patch_dir.sh* that automatically extracts a version of
the st source so that I can patch things manually very quickly.

- I typically execute `./xbps-src clean` prior to doing any manual patching
- `xbps-src extract st` is how I get the latest source instead of downloading
  from suckless's website
- Patches were downloaded to a common directory (see *Patch List* section above)
- Patches were applied in this order using `patch -Np1 -i <input_patch_name>` 
  in the patched source directory:
	- **glyph wide support**
    - **font2**:
        - changed the font and font2 pointers in the config.def.h file to desired font name
        - See *Dependencies* for the fonts used
	- **Xresources**
		- updated defaultfg, defaultbg, defaultcs, defaultrcs in config.def.h
        to map to the correct &colorname array value / Xresources element
	- **defaultfontsize**
	- **anysize**
        - glyph wide support patch did not play nice with this patch, 
          had to manually fix the rejects
    - **scrollback**
        - note, just applied the basic patch
- A couple final manual tweaks to the main config file include
    - Updating termname = xterm-256color
    - Changed zoom keys to be Ctrl+Shift+H/L/O for zoom out/in/reset
    - Changed scroll keys to be Shift+J/K for scroll down/up
- A final *overall* patch was created using `diff -Np1 <original_source_dir> <patched_source_dir> > <diff_file_Name>`
- The final *overall* patch is what is included in this repo. Follow the *Usage* section for installation instructions

## Dependencies
Since modifications to the source in my patch have a couple of assumptions, 
here are the things you must make sure are present in your system (unless they
are edited out of my patch):

- Font: Inconsolata Nerd Font (used as main font)
- Font: Inconsolata for Powerline (used in font2 as a backup)
- Font: Hack Nerd Font (used in font2 as a backup)
