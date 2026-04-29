<p align="center">
<img src="https://i.imgur.com/Q0ag9l5.png)" alt="Windows server logo"/>
</p>


<h1>Windows Server 2025 Installation & Post-Deployment Configuration (VirtualBox)</h1>
<h2>Project Overview</h2>
In this lab, I installed Windows Server 2025 Standard (Desktop Experience) on a VirtualBox virtual machine created in the previous lab.
The project included full OS installation, partitioning, initial server setup, security configuration adjustments, Guest Additions integration, system renaming, and Windows Update management. <br />


<h2> Technologies Used</h2>

- Oracle VirtualBox 7
- Windows Server 2025 Standard (Desktop Experience)
- Microsoft Azure Education (ISO & Product Key)
- Guest Additions
- Windows Update

<h2> Objectives </h2>

- Install Windows Server on a virtual machine
- Configure disk partitioning for future lab expansion
- Apply initial server setup and usability optimizations
- Configure network/workgroup identity
- Install virtualization integration tools
- Prepare the server for future networking and Active Directory labs

<h2>Installation Steps</h2>

<h3>Starting Windows Server Installation</h3>

(Warning!!: Do NOT install Windows Server on your physical machine/disk! It will overwrite the entire physical disk, erase all data on the disk, and replace the Windows version you have there!)

If you have gone through the steps i outlined in https://github.com/AYusufIT/virtualbox-vm-setup-windows-server.  The Windows Server installer will automatically start from the ISO file after the virtual machine starts. (Do NOT open the ISO file or double-click it!)

You will first see a black screen and the installer will load boot files from the ISO image.
Once the installer has loaded, you will be prompted to enter the following:
- Installation language (English only)
- Time and currency format. I selected Norwegian, feel free to choose the language that fits your time and currency.

<img src="https://i.imgur.com/HYy0Jgz.png" height="40%" width="40%" alt="Windows Sever Download steps"/>

Then
Keyboard layout (Keyboard or input method). I Selected
Norwegian but you can chose what keyboard lay out fits you. 


<img src="https://i.imgur.com/KQrS5X5.png" height="40%" width="40%" alt="Windows Sever Download steps"/>

Click Next> and then  <img src="https://i.imgur.com/N7kHU98.png" height="8%" width="8%" alt="Windows Sever Download steps"/> in the next window.
In the Select setup option screen, select Install Windows
Server


<img src="https://i.imgur.com/u6iIQBf.png " height="40%" width="40%" alt="Windows Sever Download steps"/>

In the Choosing a licensing method screen: Select Use a product key and enter the Windows Server license key that you received in Azure Dev Tools for Teaching. If you haven't yet obtained a license key, you can proceed without a key by clicking the I don't Have a Product Key link at the bottom of the screen.


<img src="https://i.imgur.com/u6iIQBf.png" height="40%" width="40%" alt="Windows Sever Download steps"/>

In the Select Image screen, select the installation option
Windows Server 2025 Standard (Desktop Experience).
This installs Windows Server with a full
graphical user interface.
Accept the license terms.


<img src="https://i.imgur.com/kECts4K.png" height="40%" width="40%" alt="Windows Sever Download steps"/>

<h3> Disk Partitioning & OS Deployment:
Selecting and partitioning the installation disk.</h3>


Now a list of disks and any partitions on them will appear. You will see the virtual hard disk as Disk 0 Unallocated space (without partitions).


<img src="https://i.imgur.com/YvkDc9d.png" height="40%" width="40%" alt="Windows Sever Download steps"/>

You will now create a new partition to install
Windows Server on:

- Select Drive 0, click Create Partition and create a new empty primary partition on Drive 0
that takes up 60 GB (60,000 MB) of the disk. Click Apply
- Windows will automatically create one smaller
partition of 100MB (Partition 1) in addition to
the main partition (Partition 2). Both have
Primary as type.
- Leave the rest of the (virtual) disk (about 20 GB)
unallocated. This space will
be used in a later exercise.
- Select the main partition (Partition 2) and click Next to install Windows Server on
it.
- Confirm that you are ready to install.


<img src="https://i.imgur.com/TOS0qw6.png" height="40%" width="40%" alt="Windows Sever Download steps"/>

Now the installation of Windows Server will start.
The installation will take several minutes, and the VM will restart
during the installation. (Do not boot from the CD / DVD now!)

After the restart, you will be asked to change the password for the
Administrator user account. Windows Server requires
passwords that contain both letters and numbers.

Use the administrator password:
Password.Server (period in the middle)


<img src="https://i.imgur.com/b6Mn44d.png" height="40%" width="40%" alt="Windows Sever Download steps"/>

Note!: In a production installation you should of course use a more secure password, but in these labs it is an advantage that you use this password so that it is easy for you to remember/find again and  You can choose a different password, but then you MUST remember it! If you forget it, you will lose access to the server and will have to install a new one!

<h3> Initial Login & ISO Removal </h2>

After booting, you can log in by sending Ctrl-Alt-Del to the virtual machine as follows:

- In VirtualBox: Use the menu option Input → Keyboard → Insert Ctrl-Alt-Del
- In VMWare: Use this button <img src="https://i.imgur.com/h4lEpJm.png" height="5%" width="5%" alt="Windows Sever Download steps"/>


Log in with the Administrator user account.After the first login, you will be asked a question about
what data you allow Microsoft to collect. Select Required only. You will be given the option to try Windows Admin Center and
Azure Arc. We will not be using them in this topic, so you can click away from this message


<img src="https://i.imgur.com/ld1HmoW.png" height="40%" width="40%" alt="Windows Sever Download steps"/>

You can now disconnect the ISO file from the optical drive as follows:

- From the VirtualBox Manager menu: Select Machine > Settings > Storage
- Highlight the DVD drive with the ISO file under Controller: SATA
- Click the DVD icon to the right of the Optical drive: SATA Port1 text
- Select Remove Disk from Virtual Drive.
- Click OK

<h2> Post-Installation Configuration  </h2>


After logging in, you will be taken to the Server Manager Dashboard:


<img src="https://i.imgur.com/R5PhRhw.png" height="50%" width="50%" alt="Windows Sever Download steps"/>



You will now configure important parameters for the new server:

Select Local Server in the menu on the left and do the following configuration:

<img src="https://i.imgur.com/kkMY9zo.png" height="50%" width="50%" alt="Windows Sever Download steps"/>

Use the link behind Windows Defender Firewall.

Close the Windows Security window

<img src="https://i.imgur.com/Q0ux3dS.png" height="40%" width="40%" alt="Windows Sever Download steps"/>

(Note!: Turn off the firewall for both Domain Network, Private Network and Public Network
The  Windows Firewall will be useful later, but for now it will only be "in the way"  in these labs,
so turn it off now.)

Use the link behind IE Enhanced Security Configuration in the
right column, and turn this off for both Administrators
and other users.

Use the link behind Timezone and set the correct time zone and
time.

<img src="https://i.imgur.com/4RpfaSv.png" height="40%" width="40%" alt="Windows Sever Download steps"/>

(Note! IE ESC is a security mechanism that blocks most websites in the Edge browser on Windows Server. In the exercises in this topic, you will use the browser on the server. Therefore, it is practical to turn off thissecurity mechanism.) 

Use the link behind Computer name in Server Manager

- Note! Use the button !
- Change Computer name to MIN_SERVER or MY_SERVER in english.
-  The machine must be a member of a workgroup named WORKGROUP

After changing the machine name, you must restart Windows
Server, and log in again

<img src="https://i.imgur.com/ioMz191.png" height="40%" width="40%" alt="Windows Sever Download steps"/>

After the VM has restarted and you have logged in again, it may be a good idea to install the Guest Additions program from Oracle. This is an additional program that comes with VirtualBox and is installed on the virtual machine. The program is required, among other things, to be able to cut and paste between the physical and virtual machines. In addition, the program will automatically scale the screen when you change the size of the window in which the VM is running.

- Select the menu item Devices → InsertGuest Additions CD image from the VirtualBox menu bar.
- Start File Explorer and open the CD on drive D.
- Run the
installation program
VBoxWindowsAdditions and follow
the instructions.
- Restart the virtual machine when the
installation program prompts you to do so and
login again after restarting.


<img src="https://i.imgur.com/dGKy8rc.png" height="40%" width="40%" alt="Windows Sever Download steps"/>

From now on, you don't have to use the Home Key to release the cursor from the virtual machine!
In addition, the screen size in Windows should now adjust automatically if you change the size
of the virtual machine window.

If the text on the virtual machine is (still) very small, you can enlarge it as follows:

- Right-click on the screen (desktop) of the virtual machine and select Display settings.
- Increase the font size to 125% under the heading Scale and layout.
-  Log out of the virtual machine and log in again.

Now is the time to update Windows Server with all new updates:

-  Start Settings from the Windows menu
- Select Windows Update
-  Windows will automatically start searching for, downloading, and installing updates.
If not: Use the button
-  Install all updates, and let the machine complete them.

The installation(s) will take a long time! You may have to restart the virtual machine and check for new
updates several times.

Shut down the virtual machine with + and Shut down when you are finished.
