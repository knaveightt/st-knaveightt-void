# st-knaveightt-void (st-0.9)
> Patched st terminal used for my workstations, provided via a patch against st-0.9 for use with xbps-src automated installation in void linux.

## Usage 
Included in this repo is a patch file which represents a full patch to the original st source. The following are usage instructions for incorporating this patch for usage in Void Linux's xbps-src build workflow, however the final patch can be used however you may normally patch st for installation into your own system. 
- copy the patch file to a *patches* directory in the `void-packages/srcpkgs/st` directory
- run `xbps-src pkg st` to build the xbps package
- install the package from the void-packages directory using `sudo xbps-install --force --repository=hostdir/binpkgs/ st`
- Recommendation is to lock the st package to the local repo so changes from the default repositories don't overwrite the package. Do this using `xbps-pkgdb -m repolock st`

## Patch List
List of included patches are as follows.
| Patch Name | Source URL |
| ---------- | ---------- |
| xresources | [https://st.suckless.org/patches/xresources/st-xresources-20200604-9ba7ecf.diff](https://st.suckless.org/patches/xresources/st-xresources-20200604-9ba7ecf.diff) |
| boxdraw    | [https://st.suckless.org/patches/boxdraw/st-boxdraw_v2-0.8.5.diff](https://st.suckless.org/patches/boxdraw/st-boxdraw_v2-0.8.5.diff) |
| defaultfontsize | [https://st.suckless.org/patches/defaultfontsize/st-defaultfontsize-20210225-4ef0cbd.diff](https://st.suckless.org/patches/defaultfontsize/st-defaultfontsize-20210225-4ef0cbd.diff) |
| anysize | [https://st.suckless.org/patches/anysize/st-anysize-20220718-baa9357.diff](https://st.suckless.org/patches/anysize/st-anysize-20220718-baa9357.diff) |

## Notes on Patch Application
- It seems to be a good idea to execute `./xbps-src clean` prior to doing any manual patching
- `xbps-src extract st` was used to download the original source code for st for use of patching
- a copy of the source directory was created and used for the actual patching
- patches were downloaded to a common directory (see *Patch List* section above)
- patches were applied using `patch -Np1 -i <input_patch_name>` in the patched source directory
	- Xresources patch specifics:
		- updated defaultfg, defaultbg, defaultcs, defaultrcs to map to the correct 
		  &colorname array value, mapping to the correct Xresources element
	- boxdraw patch specifics: none
	- defaultfontsize specifics
		- none, however I updated the font in the config.def.h file to Inconsolata Nerd Font
- A final *overall* patch was created using `diff -Np1 <original_source_dir> <patched_source_dir> > <diff_file_Name>`
- the final *overall* patch is what is included in this repo. follow the *Usage* section for installation instructions
