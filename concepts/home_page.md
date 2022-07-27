# About the Home page

The Home page is the main control center of SIP's web interface. It includes:

-   A clock showing the current time and date at the location of the controller. This also appears on all pages.
-   A navigation bar at the top for moving between pages of the interface. This is also present on the other pages except the optional login page.

    ![](./images/nav-bar.png)


-   A set of buttons for making global changes to the behavior of the system:
    -   ![](./images/system.png) for controlling the overall operation of the software.
    -   ![](./images/water-level.png) allows setting the "water Level" which is a global percentage of the run time for all irrigation programs
    -   ![](./images/rain-delay.png) allows suspending irrigation for all stations except ones that have been set to ignore rain on the **Stations page**
    -   ![](./images/manual.png) switches the system between automatic mode, and manual mode. Manual mode allows direct control of stations  
        CAUTION: Setting this to Manual mode will prevent any scheduled programs from running.

-   A time line that provides information about completed and scheduled irrigation events ![](./images/timeline.png)

    The **PREV DAY**, **TODAY** and **NEXT DAY** buttons allow you to view past irrigation logs, today's schedule and future irrigation schedules


-   ![](./images/stop-all.png) immediately cancels a running irrigation program or station

-   A footer that is present on all pages. The footer includes:
    1.  A Help button ![](./images/help_button.png) which opens a separate browser tab with content from the project's Documentation Wiki
    2.  ![](./images/temperature.png) The Temperature of the Raspberry Pi's CPU. The displayed temperature can be toggled between C and F by clicking the temperature displayed.
    3.  A link to the project's software repository and the revision number of the installed software

