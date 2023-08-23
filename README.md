> [!WARNING]
> ***GitHub LFS considered harmful***.
>
> On 2023-08-13 GitHub has permanently disabled Git LFS for ALL of our
> repositories because we've "exceeded the data plan". Instead of
> limiting downloads to the allotted bandwith, they simply let them
> run wild and then shut it down entirely.
>
> Let this be a warning to everyone (considering) using Git LFS on
> Github. They cannot be trusted. In the meantime, you can download
> `hda.img` here: https://rtts.eu/download/win311/hda.img


Virtual Machine with Windows 3.11
=================================

Here's a fully configured Windows 3.11 machine with a working internet
connection and a load of software, games, and of course [Microsoft
BOB](https://en.wikipedia.org/wiki/Microsoft_Bob) 🤓

![Screenshot of Windows 3.11](https://raw.githubusercontent.com/rtts/win311/main/screenshot.png)

The file `hda.img` contains the harddrive. You can mount it directly
with the `./mount` command to copy over files. The `./start` command
starts the machine using [QEMU](https://www.qemu.org/).

Inside QEMU, Windows 3.11 successfully connects to the internet and
offers a very pleasant browsing experience using Netscape Navigator 3
with javascript disabled. Internet Explorer 3 and 5 are also included,
but completely useless due to incorrect rendering of CSS.


Network configuration
---------------------

TCP/IP networking is made possible by the Microsoft 32 bit TCP/IP
networking stack (`tcp32b.exe`). The gateway address has been set to
`192.168.178.1`. To change it, go to `Open Accesoires -> Windows Setup
-> Options -> Change network settings` and then find your way around
vaguely familiar dialogs.

The installed driver is for the Realtek 8029 networking adapter, which
is the one that is actually emulated with QEMU's `ne2k_pci` option
(thank you Friedemann Baitinger for pointing me in the right direction
in [this 2004 forum post](https://lists.gnu.org/archive/html/qemu-devel/2004-12/msg00296.html)).


Display configuration
----------------------

After a lot of trial and error, I have finally been able to get the
Cirrus 5446 drivers to work properly. The resolution is currently set
to 1024x768 but even 1280x1024 works perfectly. You can adjust the
settings with the `WinMode` utility in the `VGA Display` group.


Persisting changes
------------------

Type `Ctrl-Alt-2` to switch to the QEMU monitor, then type `commit all`.
