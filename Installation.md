# <span class="mw-headline" id="Installation">Installation and Set UP</span>

### <span class="mw-headline" id="Requirements:">Requirements:</span>

1.  A suitable SD memory card that has been flashed with an up to date rev of the Raspbian operating system. See the Raspberry Pi [Quick Start Guide](http://www.raspberrypi.org/quick-start-guide) for instructions. Be sure the system is properly set up with the correct time zone for your location.
2.  An internet connection

### <span class="mw-headline" id="Install_git:">Install git:</span>

**Note:** If you are running a resent full version of the Raspbian operating system, git should already be installed. You can test this by typing 'git' (without quotes) in a terminal window. If git is installed you will see a help screen showing git commands. If you are running Raspbian Lite or if git does not appear to be installed follow these instructions.

With the Raspberry Pi connected to the internet, open a terminal window (command line). enter the following command:

<pre>sudo apt-get install git
</pre>

After a couple of seconds, you may be asked if you want to proceed, answer **yes** by typing **y** and the installation should finish within a minute or two.

### <span class="mw-headline" id="Quick_Program_Installation:">Quick Program Installation:</span>

Be sure you are in the Pi user's home directory (pi@raspberrypi ~ $).
 Clone the SIP directory from GitHub by issuing the following command:

<pre>git clone https://github.com/Dan-in-CA/SIP</pre>

The program is now installed and ready to run. To start the program execute:

<pre>cd SIP
sudo python3 sip.py</pre>

### <span class="mw-headline" id="Detailed_instructions:">Detailed instructions:</span>

#### <span class="mw-headline" id="Download_the_program_from_GitHub.">Download the program from GitHub.</span>

1.  Open a terminal window or connect to the pi [via ssh](http://learn.adafruit.com/adafruits-raspberry-pi-lesson-6-using-ssh).
2.  Type the command:

    <pre>git clone https://github.com/Dan-in-CA/SIP</pre>

    followed by the enter key.

    The program file should start downloading from the GitHub server.

    If you get an error message, carefully retype the command and double check that it is exactly as shown above. Also be sure the pi is connected to the internet.
3.  Check that the SIP directory was created in the proper location by typing **ls** (that's lower case LS). You should see the directory (SIP) listed as a sub-directory.

#### <span class="mw-headline" id="Start_the_program_for_testing">Start the program for testing</span>

1.  Log into the SIP sub-directory by typing:

    <pre>cd SIP</pre>

    followed by the enter key.
2.  start the program by typing the following command:

    <pre>sudo python sip.py</pre>

    followed by the enter key.

    You should see a message from the program “Starting timing loop” and a URL.

#### <span class="mw-headline" id="Open_the_program_in_a_web_browser">Open the program in a web browser</span>

On a device connected to your local network, enter the URL of your Raspberry Pi. For example, on my test system, the URL would be http://192.168.1.22. The URL of your Raspberry Pi will be different.

You should now see SIP's home page in your browser. Congratulations! The program is now installed and running.

**Note:** If you start the program while logged in via SSH and then log out of SSH, the program will be stopped. If you then try to access the program from your browser you will get an error message.

## <span class="mw-headline" id="Starting_the_program_automatically">Starting the program automatically</span>


Once the program is installed, you will probably want it to start automatically when the Raspberry Pi boots up. This will ensure that the program will be running even after recovering from a power outage.

There are a couple of ways to accomplish this. The simplest is to add some start-up commands to a file named “rc.local” which is in a directory named “/etc”. However, the recommended method for recent versions of Raspbian (jessie) is to use a script in /etc/systemd.

### <span class="mw-headline" id="The_recommended_method:">The recommended method:</span>

#### <span class="mw-headline" id="Starting_sip.py_from_a_script_in_.2Fetc.2Fsystemd">Starting sip.py from a script in /etc/systemd</span>

Here's the best way to automatically start SIP on boot instead of using /etc/rc.local. This is the preferred method and two files (sip.service and sip3.service) are included with the program distribution to make setup easy.

The advantage of using a systemd script is that you can easily stop, start, and check the status of SIP. Since /etc/rc.local is only executed on boot up, it's a little awkward to stop sip.py and start it again without rebooting or a typing bunch of commands.

1.  Copy one of the script files to /etc/systemd/system.  

	To Run SIP under Python 2  
	Run the command:  

    <pre>sudo cp SIP/sip.service /etc/systemd/system/</pre>
    
    To run SIP under Python 3  
    Run the command:
    
    <pre>sudo cp SIP/sip3.service /etc/systemd/system/</pre>
    
    For Python 3 you will also need to install the Python 3 version of  RPi.GPIO:
    
    <pre>sudo apt install python3-rpi.gpio</pre>
    
    **If this is not installed SIP will run but no stations will be activated under Python 3.**

2.  Enable sip service:  
	For Python 2:

    <pre>sudo systemctl enable sip.service</pre>
    
    For Python 3:
    
    <pre>sudo systemctl enable sip3.service</pre>

3. Reboot the Pi:

    <pre>sudo reboot</pre>

After the Pi has rebooted you should be able to go to the URL of your Pi from a device connected to your local network and access SIP's web interface.

If you open a terminal window on the Pi, or access the Pi via ssh you will not see any indication that the program is running. It started as “root” and is not visible to the standard Pi user. You can use the Pi as if the program wasn't running but be aware that a lot of additional activity may cause timing problems with SIP.

If you want to disable the auto-start, use:  
For Python 2

<pre>sudo systemctl disable sip.service</pre>

For Python 3

<pre>sudo systemctl disable sip3.service</pre>

If you are developing new features in the code you will find the **restart** command (see below) a quick way to check your changes.

#### <span class="mw-headline" id="Check_status.2C_start.2C_stop.2C_and_restart_sip.py">Check status, start, stop, and restart sip.py</span>

**Note:** if you are running SIP under Python 3 use **sip3** in the following commands.  
 
You can check if sip is running by executing the command:

<pre>systemctl status sip</pre>

To start sip, execute:

<pre>sudo systemctl start sip</pre>

To stop sip, execute:

<pre>sudo systemctl stop sip</pre>

To quickly restart the program after making changes, execute:

<pre>sudo systemctl restart sip</pre>

## using rc.local

### <span class="mw-headline" id="Quick_instructions:">Quick instructions:</span>

1.  Edit the file /etc/rc.local and add the following before the “exit 0” line:

    <pre> ### Start the SIP interval program
     cd /home/pi/SIP/
     python sip.py &</pre>

2.  Reboot the Pi.

    <pre>sudo reboot</pre>

### <span class="mw-headline" id="Detailed_instructions:_2">Detailed instructions:</span>

Nano is the name of a light weight text editor that is included with the Raspbian operating system. It is used to edit various configuration files including the rc.local file that can be used to start sip when the Pi boots up.

1.  In a terminal window type the following command:

    <pre>sudo nano /etc/rc.local</pre>

    followed by the enter key.

    This will open the file in the editor.

    You can use the keyboard arrow keys to move around and the Enter key to add new lines in the editor.

    Use the down arrow key on your keyboard to move the cursor (which appears as a highlighted box) down past most of the text to a blank line just before the line “exit 0”.
2.  Carefully type in the following:

    <pre> ### Start the SIP interval program
     cd /home/pi/SIP/
     python sip.py & </pre>

    Be sure to include all spaces and punctuation just as shown above.

    The first line is a comment that is there as a reminder of what the code does but doesn't actually perform any action.

    The third line is what actually starts the interval program. If you ever need to disable the automatic start, you can “comment out” this line by editing the file and placing a # character at the start of the line. You can then re-enable automatic start by removing the # character.

4.  After you have entered the lines as shown above, save the file by typing <tt>Ctrl + o</tt>. (that's the control key and the letter o together) followed by the Enter key.
5.  Exit the editor by typing <tt>Ctrl + x</tt>.
6.  Once you have exited the editor, reboot the Pi by typing:

    <pre>sudo reboot</pre>

    followed by the Enter key.

## <span class="mw-headline" id="Logging">Logging</span>

The logging feature included with SIP is disabled by default. This is to prevent the uncontrolled accumulation of log data.

### <span class="mw-headline" id="To_enable_logging:">To enable logging:</span>

Click the “Options” button at the top of the page. On the Options page click the triangle next to "Log" on the menu. You will be presented with a dialog containing a check box for enabling the feature.

### <span class="mw-headline" id="Set_the_maximum_number_of_records_to_keep:">Set the maximum number of records to keep:</span>

It is set to 100 records by default but you can change the value to whatever you like. When the maximum number of records has been reached, new records will continue to be added to the top of the list and the oldest records deleted from the bottom.

Setting the maximum to zero (no maximum) will allow records to accumulate until all available storage space is filled. This may effect system performance if the number of records becomes very large but it has been tested with over 1100 records without a noticeable problem. A practical setting might be the number of records you would get in a period of time such as a week or a month.

### <span class="mw-headline" id="Archiving_log_data:">Archiving log data:</span>

The Log page contains a link that allows you to download log data as a spread sheet friendly, comma separated values, (csv) text file to another device, e. g. a laptop. This provides a means of keeping a permanent archive of irrigation data in manageable size chunks. Once the file has been downloaded it can be imported in to your favorite spread sheet program for viewing, sorting, etc.
