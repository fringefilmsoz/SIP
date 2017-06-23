# Use a flash drive with SIP
Flash drives are relatively inexpensive and can be easily replaced.  

Keeping frequently modified data such as configuration and log files on a flash attached to your Pi will not only extend the life of the Pi's SD memory card, but if you ever need to re-install SIP or copy your settings to another Pi the flash drive will contain all your settings. You can even copy, view, and edit the files on the flash drive using a Windows or Mac system.  

### Moving config and log files to a USB Flash drive  

The steps needed to make an attached flash drive work with SIP include:  

1. Create a mount point for the flash drive. This is a location in the file system that gives you a “path” to the attached storage device.
2. Set up the Pi to automatically mount the storage device at boot time.
3. Copy SIP's data directory to the attached flash drive and rename the old directory.
4. Create a symbolic link from the the data directory's original location to the directory on the flash drive.  

#### Create a Mount point:  
To make a mount point named “flashdrive” at /media/flashdrive . Issue the command:  
`sudo mkdir /media/flashdrive`

You can name the new mount point anything you like but be sure to substitute the name you give it in the following steps.  

#### Mount the Storage device at Boot: 
Find the ID of the storage device you will be using. Before you plug in the flash drive, on the Pi’s command line type `df –h` . This will give you a listing of the memory usage on the Pi.

Plug in the flash drive, wait a couple of seconds, then issue the `df –h` command again. You should now see the added device with its ID as something like “/dev/sda1”.

Add the flash drive to the file system table (fstab) with the following commands:  
`sudo nano /etc/fstab`

This opens the file in the editor. Move to the end of the file and add:  
`/dev/sda1 /media/flashdrive auto auto,user,rw,exec 0 0`

Where “sda1” is the ID of the storage device and “flashdrive” is the name of the mount point you created.

Save the file and exit the editor.

Mount the drive (it will happen automatically from /etc/fstab on subsequent boots):  
`mount -a`

The next time your Pi is booted up with the storage device plugged in you should see it in the “df –h” listing and you can use it just like any other directory on the system. 

#### Copy SIP's data directory to the flash drive: 
With your attached flash drive mounted, copy SIP's data directory to the attached drive from the SIP directory (Use `cd SIP` if your are in the pi directory).  
`sudo cp -R data /media/flashdrive/`

Rename the old data directory:  
`sudo mv data data-old`

#### Create a Symbolic Link:
Issue the following command from the SIP directory:  
`sudo ln -s /media/flashdrive/data/ data`

This will create a sysmbolic link in the SIP directory that works ike the original data directory but the files are actuelly written to the flash drive.  

#### Replacing the Flash Drive:
If you ever need to replace the flash drive, copy the data directory from the old flash drive to the new one. You can copy it to a temporary loction on your Pi or use a Windows or Mac system to copy the data directory to the new drive.  

If you unplug the flash drive from the Pi, SIP will continues to run as long as it does not try to write to the log or any config file, in which case it will raise an "internal server error".  

Removing the flash drive from the Pi while it is running and then plugging it back in causes the drive to become "unmounted". It is then necessary to reboot the Pi.  

You can first unmount the flash drive with:  
`sudo umount /media/flashdrive`
(or whatever mount point you are using)
and then after plugging the flash drive back in:  
`sudo mount -a`
The drive should then continue to work without rebooting the Pi.

To avoid data loss, it is safer to shut down the pi when the flash drive will be unplugged or replaced.
