lsidrivemap
===========


Owners of a IBM M1015 / LSI 9220-8i controller can use this utility to map
controller ports to drives. 

I have a 24 bay disk chassis and use it to create a physical map of which 
drive is in which slot. 

![nas][nas]

[nas]: http://louwrentius.com/static/images/zfsnas01.jpg


The tool can also show the temperature of the drive.

Example output:

    root@nano:~# lsidrivemap temp

    | 37 | 40 | 40 | 37 |
    | 36 | 36 | 37 | 36 |
    | 35 | 37 | 36 | 36 |
    | 35 | 37 | 36 | 35 |
    | 35 | 36 | 37 | 36 |
    | 34 | 35 | 36 | 35 |

    root@nano:~# lsidrivemap disk

    | sdr  | sds  | sdt  | sdq  |
    | sdu  | sdv  | sdx  | sdw  |
    | sdi  | sdl  | sdaa | sdm  |
    | sdj  | sdk  | sdn  | sdo  |
    | sdb  | sdc  | sde  | sdf  |
    | sda  | sdd  | sdh  | sdg  |

    root@nano:~# lsidrivemap wwn

    | 5000cca23dc53843 | 5000cca23dc52fea | 5000cca23dc31656 | 5000cca23dc01655 |
    | 5000cca23dc459ee | 5000cca22bf0f4c3 | 5000cca22bef486a | 5000cca23dc51764 |
    | 5000cca23dc186cf | 5000cca23dc02062 | 5000cca23dda5a33 | 5000cca23dd398fa |
    | 5000cca23dd56dfb | 5000cca23dd3a8cd | 5000cca23dd9b7df | 5000cca23dda6ae9 |
    | 5000cca23dd04ded | 5000cca23dd54779 | 5000cca23dd59e65 | 5000cca23dd59b65 |
    | 5000cca23dd45619 | 5000cca23dd57131 | 5000cca23dd329ba | 5000cca23dd4f9d6 |

The wwn name of a drive is found in /dev/disk/by-id/

Customization
-------------

The output is based on my 24 bay drive chassis that has
six rows of four drives. You may need to customise the
'print_controller' function to suit your own needs. 

Known Issues
------------
The script reads the WWN serial from the drive and uses
it to find the drive name in /dev/disk/by-id. If the megacli
command does not return a WWN, which happens on older WD drives
for me, no data is returned.

Requirements
------------
- The script requires Python 2.7 or higher.
- LSI command line utility megacli or megacli64 (google for a download)
- put the /opt/MegaRAID/MegaCli/ directory in your path and either create
a symbolic link to MegaCli or MegaCli64 with the name of 'megacli' in that folder.


