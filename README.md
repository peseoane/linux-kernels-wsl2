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

![RescueGalicia](https://i.imgur.com/ZD7WRRX.png)

# WSL2 Latest kernel releases

In this repository you will find already compiled images of the kernel as well as its tagged source code.

The original repository is a constant testing and mixing between the official repositories of:

- https://www.kernel.org/
- https://github.com/microsoft/WSL2-Linux-Kernel

Since Microsoft does not update kernels "to the latest version" for obvious testing and optimization reasons, even images from kernel.org will not work directly on WSL2 without adaptation.

![Kernel 5.10.14-peseoane on WSL2 working](https://i.imgur.com/3luMTGJ.png)

> **PRECOMPILED KERNELS READY FOR WSL2**: https://github.com/peseoane/linux-wsl2/releases

In principle, only the most relevant images from the channels are kept up to date (as far as I can):

- mainline
- stable
- longterm

**EOL images are not supported and should not be used in a production environment.**

## Instalation (NEW WAY)
Create in your `C:\Users\YOURUSER\.wsl` a `dotfile` with the name `.wslconfig` and the following text:

```powershell
[wsl2]
kernel=C:\\WSL\\Kernel\\stable-5.12.10
```

Just put the full path to your compiled image or download.

The name is totally indiferent, if you download one of my releases `bzImage` will work with that name.

Now restart your `wsl` in `Powershell` or `cmd` with:

```powershell```powershell
wsl --shutdown
```

## Instalation (OLD WAY)

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

And just clone, choose one branch and you're ready to go with your changes.

## ¿Will work on my system?

The distributed versions are optimised for modern processors, with the following parameters and specially tuned for Intel, but works also in AMD, **i suggest you to recompile with your native system:**

```bash
export KCFLAGS="-o2 -mtune=native -pipe" KCPPFLAGS="-o2 -mtune=native -pipe make all"
```

> NOTE: this dosen't work anymore on Intel 11th gen, JUST DON'T DO THAT beacuase needs `gcc-10` and `g++-10` and the linker isn't supporter yet, default optimization is for Intel Core Duo / Xeon an 02 flag.

### ¿Where can i copy my bzimage?

Just open `\\wsl$` in file explorer, go to `linux/arch/x86/boot` and copy the `bzimage`, later copy on `C:\Windows\System32\Tools` and repeat the steps described at the start of the readme.
