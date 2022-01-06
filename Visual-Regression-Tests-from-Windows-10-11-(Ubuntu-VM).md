This page may if for someone who does most of their development on Windows and doesn't run OSX or Linux natively.  Someone like me.  It is probably the easiest way to run the visual regression tests if you are in this boat.

You will need to create a Linux box in a virtual machine.  You can run the virtual machine in either VMWare or Oracle VirtualBox as a host.  This guide shows VirtualBox, but VMWare should work similarly.

## Step 1: Enable your computer for virtualization
Before running VirtualBox, you should enable 64bit virtualization.  If you are already running virtual machines on your computer you can skip this step.  Depending on how your system was set up these steps may already be done.

### Windows settings
Boot your computer and enter the BIOS menu.  In my case, this is done by holding down the delete key before the windows system boots (ASUS).  Your system may be a little different depending on your BIOS vendor.

Virtualization is enabled in menu that looks like this (should be Enabled):

***
![BIOS1](https://imgur.com/I9wJiWq.png)
***
![BIOS2](https://imgur.com/s2QgVuT.png)
***

After your system boots, in Windows control panel, choose Programs/Turn windows features on or off.  Make sure Hypervisor is off (box is unchecked):

***
![control panel](https://imgur.com/d1ceyEG.png)
***
![hypervisor](https://imgur.com/mlAQUKk.png)

### Install VirtualBox and a virtual machine
Install VirtualBox (it's free).  Find a good Linux server image.  I used a Ubuntu image from [OSBoxes.org](https://www.osboxes.org/ubuntu/).  Download a _server_ image, it will be about 2GB.

Then add the media from your image to VirtualBox:
***
![Add media](https://imgur.com/5AKNVP9.png)
***

Now create a new virtual machine:
***
![new machine](https://imgur.com/spTjBBB.png)
***

Set the memory size to be about 1/2 of your physical memory.
***
![memory](https://imgur.com/QRDXsAY.png)
***

Choose the image you just downloaded and added to your media list as the drive:
***
![image2](https://imgur.com/QFl6NEF.png)
***

Then click 'Create'.  In the settings for the machine, you should set your processor count to how ever many physical processors on your computer (e.g. 4 for an Intel i5).  This will greatly enhance performance.
***
![CPUs](https://imgur.com/o5xhXqv.png)
***

Then start the machine.  It will boot up and dump you into a prompt, where you can login.

### Install tools
You only need a couple of tools to run vexflow. GIT:

`sudo apt install git-all`

And Node/NPM

`curl -fsSL https://deb.nodesource.com/setup_12.x | sudo -E bash -`

`sudo apt-get install -y nodejs`

**Important note**:  I was unable to get vexflow to work with the latest (16.x at the time of this writing).  The issue is with an NPM package called canvas that has a number of issues.  There may be other solutions, but I found it easiest just to install the older version of node as shown above.

`> npm -version
6.14.6
> node --version
12.18.3
`
You can use NVM if you have multiple node versions to support.

From here, 

