---
layout: post
title: Apple Time Machine Backups Over Samba

tags: Afp,Apple,Apple,Mount Disk,Nfs,Samba,Technology,Time Machine
---
For the past couple of months I have been running Mac OS X Snow Leopard (10.6) on my custom built desktop. I recently purchased a brand new MacBook Pro for use as a portable computer. All the while I have not been using Apple's automatic backup daemon, Time Machine, and basically relying on the RAID drives on my desktop for keeping all of my data safe and secure. The desktop has been having some RAID troubles that I have not been able to diagnose yet and that got me to thinking: I should really spend some time and get this backup thing working. 

I have had a <a href="http://en.wikipedia.org/wiki/Network-attached_storage">NAS appliance</a>, the <a href="http://www.dlink.com/products/?pid=509">D-Link DNS 323</a>, lying around now for a couple of months collecting dust. There are many tutorials on the Internet that make this process much harder than it actually is, attempt to explain what might go wrong and finally offer no real explanation about why it is going wrong. Now, the very first thing to remember is to run this command <em>as your user privileges</em>. Inside of the <strong>Terminal</strong> application, execute the following command and restart your Mac. 

<pre lang="sh">defaults write com.apple.systempreferences TMShowUnsupportedNetworkVolumes 1</pre>

What you need to do now is create a special disc image called a <em>sparsebundle</em>, which ideally, should be twice the size of the hard-drive that you are looking to backup. Unfortunately I do not have enough disk space available on my network for this. 

First let's go over Mac OS X Snow Leopard, where the filename of the sparsebundle needs to merely be the <em>hostname.sparsebundle</em>. A special XML file needs to be saved into the root directory of the sparsebundle package. If you are using Mac OS X Leopard (10.5) then the name of the image file needs to include the MAC address of the en0 ethernet interface. This is in a hexadecimal format. You can run the following commands to build the filename. The second command gets the username of the system. The format of the sparsebundle should be <em>hostname_macaddress.sparsebundle</em>. 

<pre lang="sh">ifconfig en0 | grep ether | cut -d' ' -f 2 | tr -d ':'
hostname -s
</pre>

The following command creates the sparsebundle package. You can create any size that you wish. Remember the last argument of the command needs to be the proper filename depending on which version of OS X you have (see above). The first command is for Leopard and the second for Snow Leopard. 

<pre lang="sh">hdiutil create -size 200g -fs HFS+J -volname "Backup of xavior" xavior_58b035fdf8f3.sparsebundle
hdiutil create -size 200g -fs HFS+J -volname "Backup of xavior" xavior.sparsebundle</pre>

This step only needs to be done for Snow Leopard. You need to run the first command to get the UUID, and place it inside of the XML file. You should save the XML file in the root directory of the sparse bundle as the following <em>xavior.sparsebundle/com.apple.TimeMachine.MachineID.plist</em>.

<pre lang="sh">ioreg -rd1 -c IOPlatformExpertDevice | awk '/IOPlatformUUID/ { split($0, line, "\""); printf("%s\n", line[4]); }'</pre>

Now place the string inside of the XML file and save it accordingly.

<pre lang="xml"><?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>com.apple.backupd.HostUUID</key>
    <string>UUID_STRING</string>
</dict>
</plist></pre>

Finally, mount the location via Samba (or any other network protocol) and copy the file over into the mounted folder. Inside of Time Machine select the mount point as the disk and let er rip. [caption id="attachment_671" align="aligncenter" width="670" caption="Mount selection for Time Machine"]<a href="http://thoughtlessbanter.com/wp-content/uploads/2010/09/Screen-shot-2010-09-12-at-8.31.52-PM.png"><img src="http://thoughtlessbanter.com/wp-content/uploads/2010/09/Screen-shot-2010-09-12-at-8.31.52-PM.png" alt="" title="Time Machine Select Disk" width="670" height="444" class="size-full wp-image-671" /></a>[/caption] 
