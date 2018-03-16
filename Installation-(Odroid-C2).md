# WiringPi setup

Setup wiringPi according [manual](https://wiki.odroid.com/odroid-c2/application_note/gpio/wiringpi)

To find out wiring PINS, run command, and look for column **Physical** for pin numbers:

`gpio readall`

Following pins are used in SIP:

`relay_pins = [11,12,13,15,16,18,22,24,26,29,31,32,33,35,36]`

# SIP setup

It was decided to keep Odroid-C2 specific code separately from main code (branch odroid-c2), so in order to use SIP on Odroid board, you need to checkout **odroid-c2** branch instead of master. 
1. Follow general installation [Wiki steps](https://github.com/Dan-in-CA/SIP/wiki/Installation).
2. Additional steps **after you clone repository and change to SIP directory**:

`git checkout odroid-c2`

Then proceed setup as in original wiki page.

**Note:** default systemd startup script will not work if you install SIP under root user. You have to fix it manually (edit file sip.service, change paths)

# Relay board plugin setup

Once up and running SIP, you need to install relay board plugin. Plugin manager will fetch general version of relay plugin  which is not adopted to work with Odroid-C2. So, after installing plugin, you will need to:
1. manually download relay board plugin from here: [here](https://github.com/egisz/sip_plugins/blob/odroid-c2/relay_board/relay_board.py) and copy it to SIP/plugins/ folder.
2. Restart SIP.
