# Extending the Life of Your SD Card
The SD memory card that holds the operating system and programs on your Raspberry Py has finite number of write cycles. This is in the range of ten thound writes for each memory location on the card. While this may seem like a lot, the card can "wear out" rather quickly if data is frequently written to it. When the card can't be written to any longer it can still be read. This will allow the installed OS and applications to continue to function but they can no nonger be updated.  

SIP was developed with this in mind. Things like logging have been keept to a minimum and the use of database programs to hold configuration data has been avoided.  

Once the operating system and programs are installed SIP writes configuration data as well as the irrigation log to simple text files.  

High quality SD cards use a tecnique called "wear leveling" to spread data writes over the available memory locations on the card. One way to ensure that the SD card in your system has a long useful life is to use a quality card from a reliable manufacturer. Using a card with a large storage capacity such as 8 or 16 gigabytes will also extend the card's life by spreading the data writes over a larger area. Be sure that the Pi's configuration has been set to use all the available space on the card.  

Another good strategy is to attach an add-on storage device such as a flash drive to the Pi and use that to hold frequently updated files.  

See [Use a flash drive with SIP](\flashdrive) details on how to use s flash drive to hold SIP's configuration and log files.