# Step-by-step installation

## Be sure Git is installed

If you are running a full version of **Respberry Pi OS with desktop environment** git should already be installed. You can test this by typing **git** in a terminal window. If git is installed you will see a help screen showing git commands. If you are running **Respberry Pi OS Lite** or if git does not appear to be installed follow the instruction below to install git.

**Remember:**
Linux commands on the Raspberry Pi are case sensitive.

-   Enter the following command on the command line:

    <pre>sudo apt install git -y</pre>

    Git installation should finish within a minute or two.

## Clone SIP from GitHub

1.  Update the OS with the following commands:

    <pre>apt update</pre>

    <pre>apt full-upgrade</pre>

    This step is optional but is highly recommended. The process may take few minutes to complete.

2.  Log into the folder where SIP will be installed. There are two recommended locations:  
    -   The opt directory where apps are normally installed \(cd /opt\).
    -   Your user's home directory \(cd ~\).  
3.  Enter the command:

    <pre>git clone https://github.com/Dan-in-CA/SIP</pre>

    When the download finishes SIP will be installed and ready to run.

4.  Log into the SIP folder

    <pre>cd SIP</pre>

5.  Start SIP for testing

    <pre>sudo python sip.py</pre>

    You will see some information about SIP's startup and operation.

6.  Get the Pi's IP address

    <pre>hostname -I</pre>


    The first part of the returned value \(up to the first space\) will be your Pi's IP address.

7.  Enter the Pi's IP address into a web browser on a system connected to the same network as the Pi.

    The home page of SIP's web based user interface \(UI\) will open.

8.  Close SIP.s browser tab.

9.  In the SIP folder run the command

    <pre>sudo ./sip_service.sh</pre>

    This will set up and enable the systemd sip.service that will automatically start SIP on boot.

10. Reboot the Pi.

    <pre>sudo reboot</pre>

    After the Pi has rebooted SIP will be up and running, ready to be connected to your irrigation / sprinkler system and programmed with your irrigation schedules. See **Opening the SIP web interface** to get started.

**Related information**  
[Installing SIP](install_info)  
[Installing Raspberry Pi OS for SIP](pi_os_for_sip)  
[SSH Access](ssh_access)  
[Using the install script](using_install.sh) 
[Opening the SIP web interface](ui_access)  
[Home](Home)