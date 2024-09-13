Mon Sep 2 2024


# Compilation on ARM based systems

So the binary created by the makefile generates it for the X86_64, if compiled normally, however we needed it for ARM.


First i started to look for ways to cross-compile without needing an ARM machine, however i quickly realized that wasn't possible without extra unnecessary efforts.

The code i wrote myself was architecture-independant, that means it could be compiled on any architecture, however the libraries which were needed to cross compile were not installed on my system.

I attempted to install them via aptitude, however it simply did not work. Installing them manually using .deb wasnt possibe either, installing them forcefully would just break my system so i started looking for ARM builders on github.



First i looked for GitHub hosted runners, they had no ARM machines available, or those available were paid. Therefore i switched to compiling on an ARM based virtual machine.


# Attemping to setup an ARM virtual machine on VMware and Virtualbox

I went to https://deb.debian.org/distrib and downloaded an ARM version of the ISO, however while attempting to install it on VMWare and Virtualbox, both showed it as Other/Linux.

Attempting to boot failed since it said the ARM architecture was not supported.

I quickly looked up on the internet and found out that ARM architecture in VMWare was only possible on Apple Macintosh. It made total sense since ARM is a propritery architecture, and Macs are ARM based.

# Setting up ARM in Qemu

Qemu supports ARM virtual machines, therefore i installed it alongwith virt-manager. I installed the image and after some time it installed successfully.

(To be continued ..)
