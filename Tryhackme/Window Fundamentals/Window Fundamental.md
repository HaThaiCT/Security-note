# Window Editions
The Windows operating system has a long history dating back to 1985, and currently, it is the dominant operating system in both home use and corporate networks. Because of this, Windows has always been targeted by hackers & malware writers.

Windows XP was a popular version of Windows and had a long-running. Microsoft announced Windows Vista, which was a complete overhaul of the Windows operating system. There were many issues with Windows Vista. It wasn't received well by Windows users, and it was quickly phased out.

When Microsoft announced the end-of-life date for Windows XP, many customers panicked. Corporations, hospitals, etc., scrambled and tested the next viable Windows version, which was Windows 7, against many other hardware and devices. Vendors had to work against the clock to ensure their products worked with Windows 7 for their customers. If they couldn't, their customers had to break their agreement and find another vendor that upgraded their products to work with Windows 7. It was a nightmare for many, and Microsoft took note of it.

Windows 7, as quickly as it was released soon after, was marked with an end of support date. Windows 8.x came and left and it was short-lived, like Vista.

Then arrived [Windows 10](https://www.microsoft.com/en-us/windows/features?activetab=NewPopular), which is the current Windows operating system version for desktop computers.

Windows 10 comes in 2 flavors, Home and Pro. You can read the difference between the Home and Pro [here](https://www.microsoft.com/en-us/windows/compare-windows-10-home-vs-pro). 

Even though we didn't talk about servers, the current version of the Windows operating system for servers is [Windows Server 2019](https://www.microsoft.com/en-us/windows-server).

Many critics like to bash on Microsoft, but they have made long strides to improve the usability and security with each new version of Windows.

**Note**: The Windows edition for the attached VM is Windows Server 2019 Standard, as seen in **System Information**.

**Update**: As of June 2021, Microsoft announced the retirement dates for Windows 10 [here](https://docs.microsoft.com/en-us/lifecycle/products/windows-10-home-and-pro?ranMID=24542&ranEAID=kXQk6*ivFEQ&ranSiteID=kXQk6.ivFEQ-M28j3qbUhtM2JFCT2wmhOA&epi=kXQk6.ivFEQ-M28j3qbUhtM2JFCT2wmhOA&irgwc=1&OCID=AID2000142_aff_7593_1243925&tduid=%28ir__uszrgcddyskfqz3fkk0sohz3wv2xuurc01kgzkod00%29%287593%29%281243925%29%28kXQk6.ivFEQ-M28j3qbUhtM2JFCT2wmhOA%29%28%29&irclickid=_uszrgcddyskfqz3fkk0sohz3wv2xuurc01kgzkod00&ranMID=24542&ranEAID=kXQk6*ivFEQ&ranSiteID=kXQk6.ivFEQ-4cKUPfbv9lM_IR2EX7K_hw&epi=kXQk6.ivFEQ-4cKUPfbv9lM_IR2EX7K_hw&irgwc=1&OCID=AID2000142_aff_7593_1243925&tduid=%28ir__feexvhocigkfqna9kk0sohznb32xutanagupypus00%29%287593%29%281243925%29%28kXQk6.ivFEQ-4cKUPfbv9lM_IR2EX7K_hw%29%28%29&irclickid=_feexvhocigkfqna9kk0sohznb32xutanagupypus00). 

"_Microsoft will continue to support at least one Windows 10 Semi-Annual Channel until October 14, 2025_".

As of October 5th, 2021 - Windows 11 now is the current Windows operating system for end-users. Read more about Windows 11 [here](https://www.microsoft.com/en-us/windows?wa=wsignin1.0).

# The Deskstop(GUI)

The Windows Desktop, aka the graphical user interface or GUI in short, is the screen that welcomes you once you log into a Windows 10 machine.

Traditionally, you need to pass the login screen first. The login screen is where you need to enter valid account credentials; usually, a username & password of a preexisting Windows account on that particular system or in the Active Directory environment (if it's a domain-joined machine). 

![](https://assets.tryhackme.com/additional/win-fun1/win-desktop2.png)  

The above screenshot is an example of a typical Windows Desktop. Each component that makes up the GUI is explained briefly below.

1. The Desktop
2. Start Menu
3. Search Box (Cortana)
4. Task View
5. Taskbar
6. Toolbars
7. Notification Area

**The Desktop**

The desktop is where you will have shortcuts to programs, folders, files, etc. These icons will either be well organized in folders sorted alphabetically or scattered randomly with no specific organization on the desktop. In either case, these items are typically placed on the desktop for quick access.

The look and feel of the desktop can be changed to suit your liking. By right-clicking anywhere on the desktop, a context menu will appear. This menu will allow you to change the sizes of the desktop icons, specify how you want to arrange them, copy/paste items to the desktop, and create new items, such as a folder, shortcut, or text document.

![](https://assets.tryhackme.com/additional/win-fun1/win-desktop-menu.png)  

Under **Display settings**, you can make changes to the screen's resolution and orientation. In case you have multiple computer screens, you can make configurations to the multi-screen setup here. 

![](https://assets.tryhackme.com/additional/win-fun1/win-desktop-setdisplay.png)  

**Note**: In a Remote Desktop session, some of the display settings will be disabled. 

![](https://assets.tryhackme.com/additional/win-fun1/win-display-settings.png)  

You can also change the wallpaper by selecting **Personalize**.

![](https://assets.tryhackme.com/additional/win-fun1/win-desktop-personalize.png)  

Under Personalize, you can change the background image to the Desktop, change fonts, themes, color scheme, etc. 

![](https://assets.tryhackme.com/additional/win-fun1/win-personalize-settings.png)  

**The Start Menu**

In previous versions of Windows, the word **Start** was visible at the bottom left corner of the desktop GUI. In modern versions of Windows, such as Windows 10, the word 'Start' doesn't appear anymore, but rather a Windows Logo is shown instead. Even though the look of the Start Menu has changed, its overall purpose is the same. 

The Start Menu provides access to all the apps/programs, files, utility tools, etc., that are most useful. 

Clicking on the Windows logo, the Start Menu will open. The Start Menu is broken up into sections. See below.

![](https://assets.tryhackme.com/additional/win-fun1/win-start-menu.png)  

8. This section of the Start Menu provides quick shortcuts to actions that you can perform with your account or login session, such as making changes to your user account, lock your screen, or signing out of your account. Other shortcuts specific to your account are your Documents (document icon) folder and Pictures folder (pictures icon). Lastly, the gear/cog icon will take you to the Settings screen, and the power icon will allow you to Disconnect from a [Remote Desktop](https://community.windows.com/en-us/stories/work-from-anywhere-with-windows-10-remote-desktop) session, shut down the computer, or restart the computer.  

In the below image, you can see what each of the icons represents. To expand this section, click on the icon that resembles a hamburger at the top.  

![](https://assets.tryhackme.com/additional/win-fun1/win-start-hamburger.png)

9. This section will show all **Recently added** apps/programs at the top and all the installed apps/programs (that are configured to appear in the Start Menu). In this section, you'll also see the apps/programs will be listed in alphabetical order. Each letter will have its own section. See below.

![](https://assets.tryhackme.com/additional/win-fun1/win-start-programs.png)  

In the above image, the first box is where the recently added apps/programs will appear. The second box is where all the installed apps/programs will appear. 

**Note**: In your VM, Google Chrome will not show up as a Recently Added program anymore.

If you have a LONG list of installed apps/programs, you can jump to a particular section in the list by clicking on the letter headings to launch an alphabet grid. See below.

![](https://assets.tryhackme.com/additional/win-fun1/win-start-grid.png)  

**Note**: The white letters match the letter headings. 

10. The right side of the Start Menu is where you will find icons for specific apps/programs or utilities. These icons are known as **tiles**. Some tiles are added to this section by default. If you right-click any of the tiles, you guessed it; a menu will appear to allow you to perform more actions on the selected tile; such as resizing the tile, unpinning from Start Menu, view its Properties, etc. See below.

![](https://assets.tryhackme.com/additional/win-fun1/win-start-tile.png)  

Apps/programs can be added to this Start Menu section by right-clicking the app/program and selecting Pin to Start. See below.

![](https://assets.tryhackme.com/additional/win-fun1/win-start-pin.png)  

![](https://assets.tryhackme.com/additional/win-fun1/win-start-pin2.png)  

**The Taskbar**

Some of the components are enabled and visible by default. The Toolbar (6), for example, was enabled for demonstration purposes.  

If you're like me and want to disable some of these components, you can right-click on Taskbar to bring up a context menu that will allow you to make changes.

![](https://assets.tryhackme.com/additional/win-fun1/win-taskbar1.png)  

Any apps/programs, folders, files, etc., that you open/start will appear in the taskbar. 

![](https://assets.tryhackme.com/additional/win-fun1/win-taskbar-chrome.png)  

Hovering over the icon will provide a preview thumbnail, along with a tooltip. This  tooltip is handy if you have many apps/programs open, such as Google Chrome, and you wish to find which instance of Google Chrome is the one you need to bring in to focus. 

When you close any of these items, they will disappear from the taskbar (unless you explicitly pinned it to the taskbar). 

**The Notification Area**

The Notification Area, which is typically located at the bottom right of the Windows screen, is where the date and time are displayed. Other icons possibly visible in this area is the volume icon, network/wireless icon, to name a few. Icons can be either added or removed from the Notification Area in Taskbar settings. 

![](https://assets.tryhackme.com/additional/win-fun1/win-taskbar-settings.png)  

From there, scroll down to the Notification Area section to make changes. 

![](https://assets.tryhackme.com/additional/win-fun1/win-taskbar-notifarea.png)  

Here are Microsoft's brief documents for the [Start Menu](https://support.microsoft.com/en-us/windows/see-what-s-on-the-start-menu-a8ccb400-ad49-962b-d2b1-93f453785a13) and  [Notification Area](https://support.microsoft.com/en-us/windows/customize-the-taskbar-notification-area-e159e8d2-9ac5-b2bd-61c5-bb63c1d437c3#WindowsVersion=Windows_10).

**Tip**: You can right-click any folder, file, app/program, or icon to view more information or perform other actions on the clicked item.

# The File System

The file system used in modern versions of Windows is the **New Technology File System** or simply [NTFS](https://docs.microsoft.com/en-us/windows-server/storage/file-server/ntfs-overview).

Before NTFS, there was **FAT16/FAT32** (File Allocation Table) and **HPFS** (High Performance File System). 

You still see FAT partitions in use today. For example, you typically see FAT partitions in USB devices, MicroSD cards, etc. but traditionally not on personal Windows computers/laptops or Windows servers.

NTFS is known as a journaling file system. In case of a failure, the file system can automatically repair the folders/files on disk using information stored in a log file. This function is not possible with FAT.   

NTFS addresses many of the limitations of the previous file systems; such as: 

- Supports files larger than 4GB
- Set specific permissions on folders and files
- Folder and file compression
- Encryption ([Encryption File System](https://docs.microsoft.com/en-us/windows/win32/fileio/file-encryption) or **EFS**)

If you're running Windows, what is the file system your Windows installation is using? You can check the Properties (right-click) of the drive your operating system is installed on, typically the C drive (C:\).

 ![](https://assets.tryhackme.com/additional/win-fun1/win-file-system.gif)

You can read Microsoft's official documentation on FAT, HPFS, and NTFS [here](https://docs.microsoft.com/en-us/troubleshoot/windows-client/backup-and-storage/fat-hpfs-and-ntfs-file-systems). 

Let's speak briefly on some features that are specific to NTFS. 

On NTFS volumes, you can set permissions that grant or deny access to files and folders.

The permissions are:

- **Full control**
- **Modify**
- **Read & Execute**
- **List folder contents**
- **Read**
- **Write**

The below image lists the meaning of each permission on how it applies to a file and a folder. (credit [Microsoft](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/bb727008\(v=technet.10\)?redirectedfrom=MSDN))

![](https://assets.tryhackme.com/additional/win-fun1/ntfs-permissions1.png)  

How can you view the permissions for a file or folder?

- Right-click the file or folder you want to check for permissions.
- From the context menu, select `Properties`.
- Within Properties, click on the `Security` tab.
- In the `Group or user names` list, select the user, computer, or group whose permissions you want to view.

In the below image, you can see the permissions for the `Users` group for the Windows folder. 

![](https://assets.tryhackme.com/additional/win-fun1/windows-folder-permissions.png)  

Refer to the Microsoft documentation to get a better understanding of the NTFS permissions for Special Permissions.

Another feature of NTFS is **Alternate Data Streams** (**ADS**).  

Alternate Data Streams (ADS) is a file attribute specific to Windows NTFS (New Technology File System).

Every file has at least one data stream (`$DATA`), and ADS allows files to contain more than one stream of data. Natively [Window Explorer](https://support.microsoft.com/en-us/windows/what-s-changed-in-file-explorer-ef370130-1cca-9dc5-e0df-2f7416fe1cb1) doesn't display ADS to the user. There are 3rd party executables that can be used to view this data, but [Powershell](https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.1) gives you the ability to view ADS for files.

From a security perspective, malware writers have used ADS to hide data.

Not all its uses are malicious. For example, when you download a file from the Internet, there are identifiers written to ADS to identify that the file was downloaded from the Internet.

To learn more about ADS, refer to the following link from MalwareBytes [here](https://blog.malwarebytes.com/101/2015/07/introduction-to-alternate-data-streams/). 

**Bonus**: If you wish to interact hands-on with ADS, I suggest exploring Day 21 of [Advent of Cyber 2](https://tryhackme.com/room/adventofcyber2).


# The Window\System32 Folders

The Windows folder (`C:\Windows`) is traditionally known as the folder which contains the Windows operating system. 

The folder doesn't have to reside in the C drive necessarily. It can reside in any other drive and technically can reside in a different folder.

This is where environment variables, more specifically system environment variables, come into play. Even though not discussed yet, the system  environment variable for the Windows directory is `%windir%`.

Per [Microsoft](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_environment_variables?view=powershell-7.1), "_Environment variables store information about the operating system environment. This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders_".

There are many folders within the 'Windows' folder. See below.

![](https://assets.tryhackme.com/additional/win-fun1/windows-folder.png)  

One of the many folders is **System32**. 

![](https://assets.tryhackme.com/additional/win-fun1/windows-system32.png)  

The System32 folder holds the important files that are critical for the operating system.

You should proceed with extreme caution when interacting with this folder. Accidentally deleting any files or folders within System32 can render the Windows OS inoperational. Read more about this action [here](https://www.howtogeek.com/346997/what-is-the-system32-directory-and-why-you-shouldnt-delete-it/). 

**Note**: Many of the tools that will be covered in the Windows Fundamentals series reside within the System32 folder.

# User Account, Profiles and Permissions

User accounts can be one of two types on a typical local Windows system: **Administrator** & **Standard User**. 

The user account type will determine what actions the user can perform on that specific Windows system. 

- An Administrator can make changes to the system: add users, delete users, modify groups, modify settings on the system, etc. 
- A Standard User can only make changes to folders/files attributed to the user & can't perform system-level changes, such as install programs.

You are currently logged in as an Administrator. There are several ways to determine which user accounts exist on the system. 

One way is to click the `Start Menu` and type `Other User`. A shortcut to `System Settings > Other users` should appear. 

![](https://assets.tryhackme.com/additional/win-fun1/win-other-user1.png)  

If you click on it, a Settings window should now appear. See below.

![](https://assets.tryhackme.com/additional/win-fun1/win-other-user.png)  

Since you're the Administrator, you see an option to **Add someone else to this PC**.

**Note**: A Standard User will not see this option.  

Click on the local user account. More options should appear: **Change account type** and **Remove**. 

![](https://assets.tryhackme.com/additional/win-fun1/win-other-user2.png)  

Click on Change account type. The value in the drop-down box (or the highlighted value if you click the drop-down) is the current account type. 

![](https://assets.tryhackme.com/additional/win-fun1/win-other-user3.png)

When a user account is created, a profile is created for the user. The location for each user profile folder will fall under is C:\Users.

For example, the user profile folder for the user account Max will be C:\Users\Max.

The creation of the user's profile is done upon initial login. When a new user account logs in to a local system for the first time, they'll see several messages on the login screen. One of the messages, User Profile Service, sits on the login screen for a while, which is at work creating the user profile. See below.

 ![](https://assets.tryhackme.com/additional/win-fun1/win-profile-service.png)

Once logged in, the user will see a dialog box similar to the one below (again), indicating that the profile is in creation.

![](https://assets.tryhackme.com/additional/win-fun1/win-profile-service2.png)  

Each user profile will have the same folders; a few of them are:

- Desktop
- Documents
- Downloads
- Music
- Pictures

Another way to access this information, and then some, is using **Local User and Group Management**. 

Right-click on the Start Menu and click **Run**. Type `lusrmgr.msc`. See below

![](https://assets.tryhackme.com/additional/win-fun1/win-lusrmgr.gif)  

**Note**: The Run Dialog Box allows us to open items quickly. 

Back to lusrmgr, you should see two folders: **Users** and **Groups**. 

If you click on Groups, you see all the names of the local groups along with a brief description for each group. 

Each group has permissions set to it, and users are assigned/added to groups by the Administrator. When a user is assigned to a group, the user inherits the permissions of that group. A user can be assigned to multiple groups.

**Note**: If you click on **Add someone else to this PC** from **Other users**, it will open **Local Users and Management**.

# User Account Control

The large majority of home users are logged into their Windows systems as local administrators. Remember from the previous task that any user with administrator as the account type can make changes to the system.

A user doesn't need to run with high (elevated) privileges on the system to run tasks that don't require such privileges, such as surfing the Internet, working on a Word document, etc. This elevated privilege increases the risk of system compromise because it makes it easier for malware to infect the system. Consequently, since the user account can make changes to the system, the malware would run in the context of the logged-in user.

To protect the local user with such privileges, Microsoft introduced **User Account Control** (UAC). This concept was first introduced with the short-lived [Windows Vista](https://en.wikipedia.org/wiki/Windows_Vista) and continued with versions of Windows that followed.

**Note**: UAC (by default) doesn't apply for the built-in local administrator account. 

How does UAC work? When a user with an account type of administrator logs into a system, the current session doesn't run with elevated permissions. When an operation requiring higher-level privileges needs to execute, the user will be prompted to confirm if they permit the operation to run. 

Let's look at the program on the account you're currently logged into, the built-in administrator account—Right-click to view its Properties.

In the Security tab, we can see the users/groups and their permissions to this file. Notice that the standard user is not listed. 

![](https://assets.tryhackme.com/additional/win-fun1/win-wireshark.png)  

Log in as the standard user and try to install this program. To do this, you can remote desktop into the machine as the standard user account. 

**Note**: You have the username and password for the standard user. It's visible in `lusrmgr.msc`.

Before installing the program, notice the icon. Do you see the difference? When you're logged in as the standard user, the shield icon is on the program's default icon. See below.

![](https://assets.tryhackme.com/additional/win-fun1/win-wireshark.png)  

This shield icon is an indicator that UAC will prompt to allow higher-level privileges to install the program.

![](https://assets.tryhackme.com/additional/win-fun1/win-wireshark2.png)  

Double-click the program, and you'll see the UAC prompt. Notice that the built-in administrator account is already set as the user name and prompts the account's password. See below.

![](https://assets.tryhackme.com/additional/win-fun1/win-uac.png)  

After some time, if a password is not entered, the UAC prompt disappears, and the program does not install. 

This feature reduces the likelihood of malware successfully compromising your system. You can read more about [UAC](https://docs.microsoft.com/en-us/windows/security/identity-protection/user-account-control/how-user-account-control-works) here.


# Settings and the Control Panel

On a Windows system, the primary locations to make changes are the Settings menu and the Control Panel.

For a long time, the Control Panel has been the go-to location to make system changes, such as adding a printer, uninstall a program, etc. 

The Settings menu was introduced in Windows 8, the first Windows operating system catered to touch screen tablets, and is still available in Windows 10. As a matter of fact, the Settings menu is now the primary location a user goes to if they are looking to change the system. 

There are similarities and differences between the two menus. Below are screenshots of each.

**Settings**:

![](https://assets.tryhackme.com/additional/win-fun1/win-settings.png)

**Control Panel**: 

![](https://assets.tryhackme.com/additional/win-fun1/win-control-panel.png)  

**Note**: The icons for Settings might be different in the version of Windows on your personal device. 

Both can be accessed from the Start Menu. See below.

![](https://assets.tryhackme.com/additional/win-fun1/win-settings-cp.png)  

Control Panel is the menu where you will access more complex settings and perform more complex actions. In some cases, you can start in Settings and end up in the Control Panel.

For example, in Settings, click on **Network & Internet**. From here, click on **Change adapter options**. 

![](https://assets.tryhackme.com/additional/win-fun1/win-change-adapter1.png)  

Notice that the next window that pops up is from the Control Panel. 

![](https://assets.tryhackme.com/additional/win-fun1/win-change-adapter2.png)  

If you're unclear which to open if you wish to change a setting, use the Start menu and search for it. 

In the example below, the search was 'wallpaper.' Notice that few results were returned. 

![](https://assets.tryhackme.com/additional/win-fun1/win-change-wallpaper.png)  

If we click on the Best match, a window to the Settings menu appears to make changes to the wallpaper. 

![](https://assets.tryhackme.com/additional/win-fun1/win-change-wallpaper2.png)

# Task Manager
The last subject that will be touched on in this module is the **Task Manager**.

The Task Manager provides information about the applications and processes currently running on the system. Other information is also available, such as how much CPU and RAM are being utilized, which falls under **Performance**. 

You can access the Task Manager by right-clicking the taskbar. 

![](https://assets.tryhackme.com/additional/win-fun1/win-task-manager.png)  

Task Manager will open in Simple View and won't show much information. 

![](https://assets.tryhackme.com/additional/win-fun1/win-task-manager2.png)  

Click on `More details`, and the view changes.

![](https://assets.tryhackme.com/additional/win-fun1/win-task-manager3.png)  

You can refer to this [blog post](https://www.howtogeek.com/405806/windows-task-manager-the-complete-guide/) for more detailed information about the Task Manager.

If you wish to learn more about the core Windows processes and what each process is responsible for, visit the [Core Windows Processes room](https://tryhackme.com/jr/btwindowsinternals).


# System Configuration

The **System Configuration** utility (`MSConfig`) is for advanced troubleshooting, and its main purpose is to help diagnose startup issues. 

Reference the following document [here](https://docs.microsoft.com/en-us/troubleshoot/windows-client/performance/system-configuration-utility-troubleshoot-configuration-errors) for more information on the System Configuration utility. 

There are several methods to launch System Configuration. One method is from the Start Menu.

![](https://assets.tryhackme.com/additional/win-fun2/msconfig-start.png)  

**Note**: You need local administrator rights to open this utility. 

The utility has five tabs across the top. Below are the names for each tab. We will briefly cover each tab in this task. 

1. General
2. Boot
3. Services
4. Startup
5. Tools

![](https://assets.tryhackme.com/additional/win-fun2/msconfig1.png)  

In the **General** tab, we can select what devices and services for Windows to load upon boot. The options are: **Normal**, **Diagnostic**, or **Selective**. 

In the **Boot** tab, we can define various boot options for the Operating System. 

![](https://assets.tryhackme.com/additional/win-fun2/msconfig2.png)  

The **Services** tab lists all services configured for the system regardless of their state (running or stopped). A service is a special type of application that runs in the background.  

![](https://assets.tryhackme.com/additional/win-fun2/msconfig3.png)  

In the **Startup** tab, you won't see anything interesting in the attached VM.  Below is a screenshot of the Startup tab for **MSConfig** from my local machine. 

![](https://assets.tryhackme.com/additional/win-fun2/msconfig4.png)  

As you can see, Microsoft advises using **Task Manager (**`taskmgr`**)** to manage (enable/disable) startup items. The System Configuration utility is **NOT** a startup management program. 

**Note**: If you open Task Manager for the attached VM, you will notice that Task Manager doesn't show a Startup tab. 

There is a list of various utilities (tools) in the Tools tab that we can run to configure the operating system further. There is a brief description of each tool to provide some insight into what the tool is for. 

![](https://assets.tryhackme.com/additional/win-fun2/msconfig5.png)  

Notice the **Selected command** section. The information in this textbox will change per tool.

To run a tool, we can use the command to launch the tool via the run prompt, command prompt, or by clicking the `Launch` button.