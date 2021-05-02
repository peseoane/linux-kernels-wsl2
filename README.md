**NOTE:** All the builds I do adapted to work on Microsoft WSL2 **are free of course**.

This takes time, testing, looking for bugs, unifying the torvalds/linux repositories with microsoft/WSL2-Linux-Kernel (which are way behind) so you always have the latest kernels, but it's work time, electricity costs... the usual stuff.

**If you want to thank me in any way, you can help the animal protection organisation of my city in Spain, @rescuegalicia**

In Spain, the abandonment of animals due to the fact that the state of alarm is over and that they are no longer valid for breaking the government's curfew, has saturated our animal shelters.

> 🦮🐶🐩😻 🐕‍🦺 **Consider donating 1€ to them if my work has been useful to you via this direct link I have created: https://www.facebook.com/donate/119500610152971/**

Their websites are:

https://www.instagram.com/rescuegalicia/
https://rescuegalicia.protecms.com/
https://rescuegalicia.protecms.com/

**Thank you very much!** 😊

# WSL2 Latest kernel releases

This linux kernel fork has the sole purpose of leaving the bzimage files in the releases section to update the kernel in Debian-based distributions for WSL2.

> **NOTE** From 28 February 2021, only images of the most recent versions of:
> * Mainline
> * Stable
> * Longterm

![Kernel 5.10.14-peseoane on WSL2 working](https://i.imgur.com/3luMTGJ.png)

Microsoft still in version 4, and 5 is alpha, if you don't wanna deal with the compilation, go to the releases folder.
> **PRECOMPILED KERNELS READY FOR WSL2**: https://github.com/peseoane/linux-wsl2/releases

## Instalation

To update the kernel, from PowerShell you must invoke the following command:

```powershell
wsl --shutdown
```
Once you have done this, open the folder: `C:\Windows\System32\Tools`

Where you **must rename the kernel file to kernel.old or whatever you want**, and the **bzimage file to kernel**.

## Custom compilation

As always, you need the dev-kit, in Ubuntu or Debian just do:

```bash
sudo apt-get install build-essential libncurses-dev bison flex libssl-dev libelf-dev
```

Later, you can git clone https://github.com/torvalds/linux or go to https://www.kernel.org/ and download your preferred version.

**I don't include the kernel source beacause all you need from this repo is just de .config file to work with WSL2.**

If you want to autocompile your version, this fork has a .config adapted to work with WSL2.

Just enter in `make menuconfig` and change values at your choice.

### ¿CCACHE?

Just change to 

```bash
time KBUILD_BUILD_TIMESTAMP='' make CC="ccache gcc" -j$(nproc)
```

## ¿Will work on my system?

The distributed versions are optimised for modern processors, with the following parameters and specially tuned for Intel, but works also in AMD, **i suggest you to recompile with your native system:**

```bash
export KCFLAGS="-o2 -mtune=native -pipe" KCPPFLAGS="-o2 -mtune=native -pipe make all"
```

> NOTE: if you clone from the git of Tolvards/Linux and not wget from Kernel ORG, the export flags will take longer, don't know why... better download from kernel.org! It's fast and the results are the same. Algo o3 flags seems fine... 0fast the same, but my releases are o2 for stable and -g por debug developer releases candidates!

### ¿Where can i copy my bzimage?

Just open `\\wsl$` in file explorer, go to `linux/arch/x86/boot` and copy the `bzimage`, later copy on `C:\Windows\System32\Tools` and repeat the steps described at the start of the readme.
