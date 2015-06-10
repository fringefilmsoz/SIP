# Installation and Set UP

### Requirements:

1.  A suitable SD memory card that has been flashed with an up to date rev of the Raspbian operating system. See the Raspberry Pi **[Quick Start Guide](http://www.raspberrypi.org/quick-start-guide)** for instructions. **Be sure the system is properly set up with the correct time zone for your location.**
2.  An internet connection

### Install git:

**Note:** If you are running a recent version of the Raspbian operating system, git should already be installed. You can test this by typing 'git' (without quotes) in a terminal window. If git is installed you will see a help screen showing git commands. Otherwise follow these instructions:

With the Raspberry Pi connected to the internet, open a terminal window (command line). enter the following command:

<pre>sudo apt-get install git
</pre>

After a couple of seconds, you may be asked if you want to proceed, answer **yes** by typing **y** and the installation should finish within a minute or two.

### Quick Program Installation:

Be sure you are in the Pi user's home directory (pi@raspberrypi ~ $).
 Clone the SIP directory from GitHub by issuing the following command:

<pre>git clone https://github.com/Dan-in-CA/SIP</pre>

The program is now installed and ready to run. To start the program execute:

<pre>cd SIP
sudo python sip.py</pre>

### Detailed instructions:

#### Download the program from GitHub.

1.  Open a terminal window or connect to the pi **[via ssh](http://learn.adafruit.com/adafruits-raspberry-pi-lesson-6-using-ssh)**.
2.  Type the command:

    <pre>git clone https://github.com/Dan-in-CA/SIP</pre>

    followed by the enter key.

    The program file should start downloading from the GitHub server.

    If you get an error message, carefully retype the command and double check that it is exactly as shown above. Also be sure the pi is connected to the internet.
3.  Check that the SIP directory was created in the proper location by typing **ls** (that's lower case LS). You should see the directory (SIP) listed as a sub-directory.

#### Start the program for testing

1.  Log into the SIP sub-directory by typing:

    <pre>cd SIP</pre>

    followed by the enter key.
2.  start the program by typing the following command:

    <pre>sudo python sip.py</pre>

    followed by the enter key.

    You should see a message from the program “Starting timing loop” and a URL.

#### Open the program in a web browser

On a device connected to your local network, enter the URL of your Raspberry Pi. For example, on my test system, the URL would be http://192.168.1.22. The URL of your Raspberry Pi will be different.

You should now see the SIP Login page in your browser. Enter the default password **"opendoor"** (without the quotes) and you should be taken to the program's Home page. Congratulations! The program is now installed and running.

**Note:** If you start the program while logged in via SSH and then log out of SSH, the program will be stopped. If you then try to access the program from your browser you will get an error message.

## Starting the program automatically

Once the program is installed, you will probably want it to start automatically when the Raspberry Pi boots up. This will ensure that the program will be running even after recovering from a power outage.

There are a couple of ways to accomplish this. The simplest is to add some start-up commands to a file named “rc.local” which is in a directory named “/etc”. However, the recommended method is to use a script in /etc/init.d. See the **[Recommended method](##The-recommended-method:)** below.

### Quick instructions:

1.  Edit the file **/etc/rc.local** and add the following before the “exit 0” line:

    <pre> ### Start the SIP interval program
     cd /home/pi/SIP/
     python sip.py &</pre>

2.  Reboot the Pi.

    <pre>sudo reboot</pre>

### Detailed instructions:

Nano is the name of a light weight text editor that is included with the Raspbian operating system. It is used to edit various configuration files including the rc.local file that can be used to start the Python interval program when the Pi boots up.

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

After the Pi has rebooted you should be able to go to the URL of your Pi from a device connected to your local network and access SIP's web interface.

If you open a terminal window on the Pi, or access the Pi via ssh you will not see any indication that the program is running. It started as “root” and is not visible to the standard Pi user. You can use the Pi as if the program wasn't running but be aware that a lot of additional activity may cause timing problems with SIP.

### The recommended method:

#### Starting sip.py from a script in /etc/init.d

Here's a better way to automatically start sip.py on boot instead of using /etc/rc.local. This is the preferred method and a file (sip.sh) is included with the program distribution to make setup easy.

The advantage of using an /etc/init.d script is that you can easily stop, start, and check the status of sip.py. Since /etc/rc.local is only executed on boot up, it's a little awkward to stop sip.py and start it again without rebooting or a typing bunch of commands. The script was adapted from the Debian skeleton template in /etc/init.d.

1.  Move the script file to /etc/init.d and rename it to sip (without the .sh extension). Log into the SIP directory and run the command:

    <pre>sudo mv sip.sh /etc/init.d/sip</pre>

2.  Make the script executable:

    <pre>sudo chmod +x /etc/init.d/sip</pre>

3.  Activate auto start on boot:

    <pre>sudo update-rc.d sip defaults</pre>

If you want to disable the auto-start, use:

<pre>sudo update-rc.d sip remove</pre>

If you are developing new features in the code you will find the **restart** command (see below) a quick way to check your changes.

#### Check status, start, stop, and restart sip.py

If you are using the sip script in /etc/init.d, as described above, you can check if SIP is running by executing the command:

<pre>service sip status</pre>

To start SIP, execute:

<pre>sudo service sip start</pre>

To stop SIP, execute:

<pre>sudo service sip stop</pre>

To quickly restart the program after making changes, execute:

<pre>sudo service sip restart</pre>

## Logging

The logging feature included with SIP is disabled by default. This is to prevent the uncontrolled accumulation of log data.

### To enable logging:

Click the “Options” button at the top of the page. On the Options page click the triangle next to "Logging" on the menu. You will be presented with a dialog containing a check box for enabling the feature.

### Set the maximum number of records to keep:

It is set to 100 records by default but you can change the value to whatever you like. When the maximum number of records has been reached, new records will continue to be added to the top of the list and the oldest records deleted from the bottom.

Setting the maximum to zero (no maximum) will allow records to accumulate until all available storage space is filled. This may effect system performance if the number of records becomes very large but it has been tested with over 1100 records without a noticeable problem. A practical setting might be the number of records you would get in a period of time such as a week.

### Archiving log data:

The Log page contains a link that allows you to download log data as a spread sheet friendly, comma separated values, (csv) text file to another device, e. g. a laptop. This provides a means of keeping a permanent archive of irrigation data in manageable size chunks. Once the file has been downloaded it can be imported in to your favorite spread sheet program for viewing, sorting, etc.

