# lsidrivemap



Owners of a IBM M1015 / LSI 9220-8i controller can use this utiliy to map
controller ports to drives. 

I have a 24 bay disk chassis and use it to create a physical map of which 
drive is in which slot. 

![24 bay chassis][chassis]

[chassis]: http://louwrentius.com/static/images/lsidrivemap.jpg

Example output:

    root@nano:/usr/src# ./lsidrivemap disk

    | sdn | sdo | sdp |     |
    | sdq | sdr | sdt | sds |
    | sde |     | sdl | sdi |
    | sdf | sdg | sdj | sdk |
    | sda | sdb | sdc |     |
    |     |     | sdd |     |


The tool can also show the drive temperature:

    root@nano:/usr/src# ./lsidrivemap temp

    | 28 | 32 | 35 |    |
    | 30 | 31 | 37 | 36 |
    | 29 |    | 38 | 37 |
    | 29 | 31 | 37 | 35 |
    | 28 | 36 | 36 |    |
    |    |    | 33 |    |

### Customization

The output is based on my 24 bay drive chassis that has
six rows of four drives. You may need to customise the
'print_controller' function to suit your own needs. 

### Known Issues

The script reads the WWN serial from the drive and uses
it to find the drive name in /dev/disk/by-id. If the megacli
command does not return a WWN, which happens on older WD drives
for me, no data is returned.

### Requirements

- The script requires Python 2.7 or higher.
- LSI command line utility megacli or megacli64 (google for a download)
- put the /opt/MegaRAID/MegaCli/ directory in your path and either create
a symbolic link to MegaCli or MegaCli64 with the name of 'megacli in that folder.


