# Installing Raspberry Pi OS for SIP

You will need to have a resent version of the Raspberry Pi imager app installed on your computer. A link for imager installation is included at the end of this topic..

Installing SIP requires entering a few commands using a command-line interface. A headless configuration is a simple solution and is recommended. These instructions demonstrate a recommended Raspberry Pi OS installation for use with SIP. It includes some important configuration settings that will help make SIP setup quick and easy.

1.  Insert the SD card into a card reader connected to your computer.

2.  Open the Raspberry Pi Imager app answering **Yes** in the User Account Control window that may appear on a Windows computer.

    ![](./images/Pi_imager-1.png)

3.  Click the **Choose OS** button.

    ![](./images/Pi_imager-2.png)

4.  Select **Raspberry Pi OS \(other\)**.

    ![](./images/Pi_imager-3.png)

5.  Select **Raspberry Pi OS Lite \(32 Bit\)**.

    The Lite version will use less space on the SD card and is quicker to install and upgrade.

    ![](./images/Pi_imager-4.png)

6.  Click the **CHOOSE STORAGE** button.

    ![](./images/Pi_imager-5.png)

7.  Select the device representing your SD card.

    ![](./images/Pi_imager-6.png)

8.  Click the **Advanced Options** button at the lower right corner.

    ![](./images/Pi_imager-7.png)

9.  Select the **Set hostname** and **Enable SSH** check boxes.

    For improved security replace the default hostname with something that describes your set up.

    ![](./images/Pi_imager-8.png)

10. Enter a **Username** replacing Pi with something unique you will remember and add a **passphrase**.

    Replacing the default Pi username will help improve the security of your SIP installation. For some good advice on creating a secure passphrase see the **Electronic Frontier Foundation** web site linked at the end of this topic.

    ![](./images/Pi_imager-9.png)

11. Optional: Select **Configure wireless LAN** and fill in the required fields if you plan to access SIP over WiFi.

    ![](./images/Pi_imager-10.png)

12. Enable **Set Locale settings** and verify or change the default information.

    This setting is important for proper operation of SIP.

    ![](./images/Pi_imager-11.png)

13. Click the **SAVE**button when your settings are complete.

    ![](./images/Pi_imager-12.png)

14. Click the **WRITE** button to begin installing the OS onto your SD card.

    After the write and verify operations are complete, you can remove the SD card from your computer and move it to the Raspberry Pi.


**Related information**  


[Raspberry Pi Imager](https://www.raspberrypi.com/software/)

[Electronic Frontier Foundation Secure passphrases](https://www.eff.org/dice)
