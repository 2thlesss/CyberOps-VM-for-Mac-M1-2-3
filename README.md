# CyberOps-VM-for-Mac-M1-2-3
this is a tutorial walkthrough for setting up and running the Cyberops VM for Cisco Cyber Ops Associates for CWCT

Required software - HomeBrew, Qemu, 7zip. Links to all will be provided

First off you need to log into your netacad account and navigate to https://www.netacad.com/portal/node/4035.

Download the Cyberops Workstation VM, and Security Onion.

While these are downloading, head to https://www.7-zip.org/download.html and download the latest 7zip for Mac. 

Install HomeBrew if you do not already have it. 
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

install Qemu
brew install qemu

now that your downloads are finished you will be using 7zip to open up the .ova files (i just did all these inside my download folder, you can make your own directory)
./7zz x <path_to_directory>/cyberops_workstation.ova 

Next step is to covert the needed file- the .vmdk
qemu-img convert -f vmdk -O raw <path_to_directory\ Workstation-disk001.vmdk cyberops.raw

now that this is done we have a .raw file that is ready to be used with qemu.

qemu-system-x86_64 -m 8192 -drive file=cyberops.raw,format=raw -boot d -net nic -net user -smp 4 

(this command must be run from the directory the .raw file is in)

-m is memory, please edit it based off the memory of your system. -smp is how many cores you wish to give to the vm.

qemu should open and you will have an instance of the the Cyberops Workstation
