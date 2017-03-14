
Installation
============

See [`INSTALL.md`](INSTALL.md) for installation instructions.


User Scripts
============

Google Photos
-------------

  + **Photos Step #1**
    - Delete `/media/hdd/Drive/Google Photos` directory
    - Delete directories who no start with 'YYYY-MM-DD xxxxx xxxxx...'
    - Directory structures shall be : 'YYYY-MM-DD xxxxx xxxxx...'
    - Every photos without EXIF informations need to be in right directory
    - Run script [`photos-step-1`](photos-step-1)
    - :heavy_exclamation_mark: a Google Photos backup should be in `/media/hdd/backup`
  + **Photos Step #2**
    - Verify if starred files are in the good directories
    - Be carefoul this script delete entire exif file before rewriting good date
    - Run script [`photos-step-2`](photos-step-2)
  + **Photos Step #3**
    - Run script [`photos-step-3`](photos-step-3)
    - Verify if photos are in the good directories eg `/media/hdd/photos/20XX/`
  + **Photos Step #4**
    - This script rename every photos in `/media/hdd/photos` to "IMG_XXXXX.JPG"
    - Run script [`photos-step-4`](photos-step-4)


Backup Photos
-------------

   + **Photos Flickr**
    - Delete Every photos on Flickr
    - Remove flickr.db
    - Run script [`photos-backup-flickr1`](photos-backup-flickr-1)
    - Run script [`photos-bakup-flickr2`](photos-backup-flickr-2)
   + **Google Photos**
    - Run script [`photos-backup-web`](photos-backup-web)
    - Run script [`crop`](crop) on external device
   + **Photos Backup External Device**
    - On the box eject current device
    - Power on usb device
    - Run script [`photos-backup-ext`](photos-backup-ext)


Youtube
-------

   + **Youtube Upload**
    - Copy videos files to ```/media/hdd/youtube-upload```
    - Run script [`youtube-upload`](youtube-upload)
   + **Youtube Download**
    - Create `~/.youtube.dl` file with the youtube id playlist
    - Run script [`youtube-backup`](youtube-upload)
