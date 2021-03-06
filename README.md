Sickbeard/CouchPotato MP4 automation script.
==============

**Automatically converts mkv files downloaded by sickbeard to mp4 files, and tags them with the appropriate metadata from theTVDB. Works as an extra_script, integrated with SAB, as well as a manual post-processing script.**

**Works with CouchPotato as well, tagging with the appropriate metadata from IMDb. Requires SAB**

- Requires Python 2.7 *(Does NOT work with Python 3)*
- Requires FFMPEG and FFPROBE
- Works on Windows, OSX, and Linux (Linux users make sure you're using a build of FFMPEG with the non open-source codecs, see here: https://ffmpeg.org/trac/ffmpeg/wiki/UbuntuCompilationGuide)

General Installation Instructions
--------------
1. Rename autoProcess.ini.sample to autoProcess.ini
2. Set the MP4 variables to your desired output
    - ffmpeg = Path to FFMPEG.exe
    - ffprobe = Path to FFPROBE.exe
    - output_directory = you may specify an alternate output directory (for example if you want to dump these mp4 files on iTunes and not have them integrated into your sickbeard collection)
    - output_extension = mp4/m4v (must be one of these 2)
    - delete_original = True/False
    - relocate_moov = True/False - relocates the MOOV atom to the beginning of the file for better streaming
    - ios-audio - creates a 2nd copy of an audio stream that will be iOS compatible (AAC Stereo) if the normal output will not be
    - audio-language - 3 letter language code for audio streams you wish to copy. Leave blank to copy all. Separate multiple audio streams with commas (ex: eng,spa)
    - audio-default-language - If an audio stream with an unidentified/untagged language is detected, you can default that language tag to whatever this value is (ex: eng). This is useful for many single-audio releases which don't bother to tag the audio stream as anything
    - subtitle-language - same as audio-language but for subtitles
    - subtitle-language-default - same as audio-language-default but for subtitles

SickBeard Installation Instructions
--------------
1. Open Sickbeard's config.ini in sickbeard and set your "extra_scripts" value in the general section to the full path to "python postConversion.py" using double backslashes (python C:\\Scripts\\postConversion.py). Make sure this is done while Sickbeard is not running or it will be reverted. And make sure python is registered as an environment variable/PATH
2. Set the SickBeard variables in autoProcess.ini:
    - host = Sickbeard host address (localhost)
    - port = sickbeard port (8081)
    - ssl = 0/1
    - api_key = Set this to your sickbeard API key (options -> general, enable API in sickbeard to get this key)
3. *OPTIONAL* - If you're using SAB, set your post processing script to sabToSickBeardWithConverter.py - this is not completely needed but gives the added benefit of doing the conversion from mkv to mp4 before Sickbeard sees the file in whatever folder you choose to download things to. It saves having to put in all the API information as well, and prevents the one additional refresh needed normally to have sickbeard see the properly converted file. That being said the postConversion script can handle everything on its own, so this step is just for the added benefits listed.

CouchPotato Support
--------------
1. Set your CouchPotato settings to the autoProcess.ini file
    - host = CouchPotato host address (localhost)
    - port = CouchPotato port (5050)
    - ssl = 1 if enabled, 0 if not
    - api_key = CouchPotato API Key (required)
    - username = your CouchPotato username
    - password - your CouchPotato password
2. Point your CouchPotato videos that are sent to SAB to nzbToCouchPotatoMP4.py for post processing; this will convert and tag them
3. Disable automatic checking of the renamer folder, the script will automatically notify CouchPotato when it is complete to check for new videos to be renamed and relocated. Leaving this on may cause conflicts and CouchPotato may try to relocate/rename the file before processing is completed.
    - Set "Run Every" to 0
    - Set "Force Every" to 0

Credits
--------------
This project makes use of the following projects:
- http://www.sickbeard.com/
- https://couchpota.to/
- http://sabnzbd.org/
- https://github.com/senko/python-video-converter
- https://github.com/dbr/tvdb_api
- https://code.google.com/p/mutagen/
- http://imdbpy.sourceforge.net/
- https://github.com/danielgtaylor/qtfaststart
- https://github.com/clinton-hall/nzbToMedia

Enjoy