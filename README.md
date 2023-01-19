# st-knaveightt-void (st-0.9)
> Patch used to modify the [st terminal](https://st.suckless.org) used for my workstations. This patch is provided against st-0.9 for use with xbps-src to automate patching and installation in void linux.

## Usage 
Included in this repo is a patch file which represents a collection of patches to the original st source. The following are usage instructions for incorporating this patch using Void Linux's xbps-src build workflow, however the final patch can be used any way you would normally patch st. 
- Copy the patch file to a *patches* directory in `void-packages/srcpkgs/st` 
- Run `xbps-src pkg st` to build the xbps package
- Install the package from the void-packages directory using `sudo xbps-install --force --repository=hostdir/binpkgs/ st`
- Recommendation is to lock the st package to the local repo so changes from the default repositories don't overwrite the package. Do this using `xbps-pkgdb -m repolock st`

## Patch List
List of included patches are as follows.
| Patch Name | Source URL |
| ---------- | ---------- |
| xresources | [https://st.suckless.org/patches/xresources/st-xresources-20200604-9ba7ecf.diff](https://st.suckless.org/patches/xresources/st-xresources-20200604-9ba7ecf.diff) |
| defaultfontsize | [https://st.suckless.org/patches/defaultfontsize/st-defaultfontsize-20210225-4ef0cbd.diff](https://st.suckless.org/patches/defaultfontsize/st-defaultfontsize-20210225-4ef0cbd.diff) |
| anysize | [https://st.suckless.org/patches/anysize/st-anysize-20220718-baa9357.diff](https://st.suckless.org/patches/anysize/st-anysize-20220718-baa9357.diff) |
| font2   | [https://st.suckless.org/patches/font2/st-font2-0.8.5.diff](https://st.suckless.org/patches/font2/st-font2-0.8.5.diff) |
| glyph wide support | [https://st.suckless.org/patches/glyph_wide_support/st-glyph-wide-support-20220411-ef05519.diff](https://st.suckless.org/patches/glyph_wide_support/st-glyph-wide-support-20220411-ef05519.diff) | 

## Notes on Patch Application
- It seems to be a good idea to execute `./xbps-src clean` prior to doing any manual patching
- `xbps-src extract st` was used to download the original source code for st for use of patching
- A copy of the source directory was created and used for the actual patching
- Patches were downloaded to a common directory (see *Patch List* section above)
- Patches were applied in this order using `patch -Np1 -i <input_patch_name>` in the patched source directory
	- glyph wide support: none
    - font2 patch specifics:
        - changed the font and font2 pointers in the config.def.h file to desired font name
	- Xresources patch specifics:
		- updated defaultfg, defaultbg, defaultcs, defaultrcs to map to the correct 
		  &colorname array value, mapping to the correct Xresources element
	- defaultfontsize specifics: none
	- anysize patch specifics
        - glyph wide support patch did not play nice with this patch, had to manually fix the rejects
- A final *overall* patch was created using `diff -Np1 <original_source_dir> <patched_source_dir> > <diff_file_Name>`
- The final *overall* patch is what is included in this repo. Follow the *Usage* section for installation instructions
