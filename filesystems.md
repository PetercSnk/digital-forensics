# Filesystems

## Clusters, Sectors, and Tracks

<img src="images/disk-structure.png"
    alt="image showing clusters, sectors, and tracks"
    style="background-color:grey;
        width:50%;"/>

| Label | Meaning |
|-------|---------|
|A|Track.|
|B|Sector.|
|C|Sector of track.|
|D|Cluster of sectors.|

## File Allocation Table (FAT) Boot Sector Layout

Values in FAT file systems are either stored in bytes, words (pair of bytes), or doublewords.
Note that little-endian is used for all values except strings where the first byte of a pair 
is the least significant byte, and the second byte of a pair is the most significant byte. 
This is also the case for double words.

| Offset | Length (Bytes) | Meaning |
|--------|----------------|---------|
|0x00|3|Bootsrap jump command.|
|0x03|8|OEM name.|
|0x0b|2|Bytes per sector.|
|0x0d|1|Sectors per cluster (power of 2 and less than).|
|0x0e|2|Size of reserved area, in sectors.|
|0x10|1|Number of FATs (usually 2).|
|0x11|2|Maximum number of files in the root directory.|
|0x13|2|Number of sectors in file system, 0x20 is used if 2 bytes is not large enough.|
|0x15|1|Media descriptor: 0xf0 is removable, 0xf8 is fixed.|
|0x16|2|Size of each FAT in sectors, used for FAT12/16; 0 for FAT32.|
|0x18|2|Sectors per track.|
|0x1A|2|Number of heads.|
|0x1C|4|Number of sectors before the start partition (hidden sectors).|
|0x20|4|Number of sectors in file system, will be 0 if 0x13 is non-zero.|

What comes after 0x20 depends on the type of FAT being used. FAT12 and FAT16 differs from FAT32.

### FAT12 and FAT16

| Offset | Length (Bytes) | Meaning |
|--------|----------------|---------|
|0x24|1|Drive number.|
|0x25|1|Not used.|
|0x26|1|Extended boot signature to validate next 3 fields.|
|0x27|4|Volume serial number.|
|0x2b|11|Volume label.|
|0x36|8|File system type: FAT12 or FAT16.|

### FAT32

| Offset | Length (Bytes) | Meaning |
|--------|----------------|---------|
|0x24|4|32-bit count of sectors per FAT.|
|0x28|2|External flags.|
|0x2a|2|File system version.|
|0x2c|4|Cluster number of the start of the root directory.|
|0x30|2|Sector number of the file system information sector.|
|0x32|2|Sector number of the back up boot sector.|
|0x34|12|Reserved.|
|0x40|1|Number of logical drives.|
|0x41|1|Unused.|
|0x42|1|Extended signature.|
|0x43|4|Serial number of partition.|
|0x47|11|Volume name of partition.|
|0x52|8|File system type: FAT32.|

## NTFS Boot Sector Layout

Note that NTFS also uses little-endian for all values except strings.

| Offset | Length (Bytes) | Meaning |
|--------|----------------|---------|
|0x00|3|Bootstrap jump command.|
|0x03|8|OEM ID.|
|0x0b|2|Bytes per sector.|
|0x0d|1|Sectors per cluster.|
|0x0e|2|Reserved sectors.|
|0x10|3|Reserved, this value is always 0.|
|0x13|2|Not used by NTFS.|
|0x15|1|Media descriptor.|
|0x16|2|Always 0.|
|0x18|2|Sectors per track.|
|0x1a|2|Number of heads.|
|0x1c|4|Hidden sectors.|
|0x20|4|Not used by NTFS.|
|0x24|4|Not used by NTFS.|
|0x28|8|Total sectors.|
|0x30|8|Logical cluster number for the Master File Table, file $MFT.|
|0x38|8|Logical cluster number for the Master File Table copy, file $MFTMirr.|
|0x40|4|Clusters per file record segment.|
|0x44|1|Clusters per index buffer.|
|0x45|3|Not used by NTFS.|
|0x48|8|Volume serial number.|
|0x50|4|Checksum.|
|0x54|426|Bootstrap code.|
