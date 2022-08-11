# Accessing the Pi using SSH

If you installed Raspberry Pi OS using the Imager app as described in **Installing Raspberry Pi OS for SIP**. Or if you have enabled SSH on the Pi, you should now be able to access the Pi using Secure Shell \(SSH\) from a computer running one of the following operating systems:

-   Windows 10 with October 2018 Update or later
-   Windows 11
-   MAC OS
-   Linux including from another Pi.

    **Important:**
    If you are running an older version of Windows you will need to install **Putty** if it is not already installed. There are a number of web sites with information about installing and using putty for SSH.


1.  Open a terminal window on your computer

2.  Enter the ssh command  
    Replacing **[username]** with the user name you used and **[hostname]** with the name you gave the system.

    <pre>ssh [username]@[hostname]</pre>

    The first time you access the Pi you may see a security warning. Answer **yes** to continue.

3.  Enter your user password for the Pi.

    You should now be at the command prompt and ready to send commands to the Pi.

4.  Check the IP address of the Pi

    <pre>hostname -I</pre>

    Make a note of the IP address that is shown as the first part of the response \(up to the first space\). It can be used for accessing SIP's user interface.  

**Related information**  
[Installing Raspberry Pi OS for SIP](pi_os_for_sip)  
[Using the install script](using_install.sh)  
[Step-by-step installation](install_steps)  
[Home](Home)
