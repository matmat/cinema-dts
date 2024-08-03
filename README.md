# Cinema DTS (APT-X100) File Format

## .AUD/.AUE/.APX File format
|Offset||Field|Format|Length|
|-|-|-|-|-|
|0x00|0|Film name|zstr|60|
|0x3c|60|Language|zstr|8|
|0x44|68|Studio|zstr|7|
|0x4b|75|Fall-back format|uint8|1|
|0x4c|76|Unknown|uint16_le|2|
|0x4e|78|Reel number|uint16_le|2|
|0x50|80|Serial number|uint16_le|2|
|0x52|82|Number of channels|uint16_le|2|
|0x54|84|Start DTS TC (30 fps)|bcd|1|
|0x55|85|Start second|bcd|1|
|0x56|86|Start minute|bcd|1|
|0x57|87|Start hour|bcd|1|
|0x58|88|End DTS TC (30 fps)|bcd|1|
|0x59|89|End second|bcd|1|
|0x5a|90|End minute|bcd|1|
|0x5b|91|End hour|bcd|1|

If byte 0x5c is 0x01 or 0x02, then there is an additional 40 byte header:

|Offset||Field|Format|Length|
|-|-|-|-|-|
|0x5c|92|0x01 or 0x02 if encrypted (only for .AUE/.APX)|uint8|1|
|0x5d|93|Encryption key (only for .AUE/.APX)|uint16_le|2|
|0x5f|95|Unknown watermark flag, 0x01 if enabled (only for .APX)|uint8|1|
|0x60|96|Unknown watermark flag, 0x01 if enabled (only for .APX)|uint8|1|
|0x61|97|Unused (always zero?)|-|5|
|0x66|102|Unknown watermark data (only used for .APX)|-|30|


### Film name
If the name begins with `SETUP` the disc (reel?) will auto-play without time code.  
Some systems (e.g. XD10) Some systems (e.g. XD10) reads only the first 18 bytes, but there are longer strings in the wild, e.g. `SETUP - Pink Noise Center` (26 bytes including '\0') from the ES Test Disc.

### Fall-back format
0x00 = Dolby A  
0x01 = Dolby SR  
0x02 = Academy  
0x80 = Nonsync at any position of the reel  
0x81 = Nonsync within the last minute of the reel, usually used for the last reel

See [this post](http://www.film-tech.com/cgi-bin/ubb/f1/t012390/p3.html#000033) by Michael Zarits on Film-Tech.

### Reel number
13 = Trailer, iff Serial number equals 1253  
14 = Trailer  
15 = Trailer, iff Serial number equals 1004

Everything else is a Feauture

### Serial number
Serial numbers with bit 15 set (>=32768) is DTS-ES. For both features and trailers.

## Sample files
- [DTS Trailer Disc January 30, 2004](https://archive.org/details/dts_cinema_audio_collection)
- [DTS Trailer Disc June 25, 2004](https://archive.org/details/dts_06-25-2004)
- [DTS Trailer Disc November 5, 2004](https://archive.org/details/dts_11-05-2004)
- [DTS DS3 setup disc](http://www.film-tech.com/warehouse/manuals/DS3.iso.gz)
- [DTS ES1 test disc](http://www.film-tech.com/warehouse/manuals/ES1.zip)

## Useful links
- [APT-x100 Decoder Input PlugIn for foobar2000 by Maxim V. Anisiutkin](https://sourceforge.net/projects/dvdadecoder/files/foo_input_apt-x100/)
- [MediaInfoLib/Source/MediaInfo/Audio/File_Aptx100.cpp](https://github.com/MediaArea/MediaInfoLib/blob/master/Source/MediaInfo/Audio/File_Aptx100.cpp)
- [35mm-sound repository by David Ferguson](https://github.com/davidferguson/35mm-sound)
- [DTS XD10/XD20 v2.2.06 software INSTALL disc](http://www.film-tech.com/warehouse/manuals/DTS-XD10-XD20_v2.2.06_InstallWithNotes.zip)
  - Decompiling `dts/home/dts/bin/ControlMgr` inside `xd10/dts.tar.gz` is a good way to understand the file format better
- ["DTS Extractor.exe" by Markus Lemm](http://www.film-tech.com/warehouse/manuals/DTSExtractor.zip)
- [dtsc plugins for xmms and winamp by Gary Kramlich](https://sourceforge.net/projects/in-dtsc/)
- [DTS - How to fit "Return of the King" (and other 3 disc movies) onto 2 dts discs](http://www.film-tech.com/warehouse/index.php?category=5)

### Forum threads on film-tech.com
- (2023-04-16) [DTS and serial numbers](http://www.film-tech.com/vbb/forum/digital-cinema-forum/28838-dts-and-serial-numbers)
- (2023-03-11) [DTS Special Venue list - help is welcome!](http://www.film-tech.com/vbb/forum/digital-cinema-forum/27934-dts-special-venue-list-help-is-welcome)
- (2022-08-04) [Film sound codec bitrate](http://www.film-tech.com/vbb/forum/digital-cinema-forum/22725-film-sound-codec-bitrate)
- (2022-06-13) [Dts tcr 1.46](http://www.film-tech.com/vbb/forum/digital-cinema-forum/21559-dts-tcr-1-46)
- (2022-02-28) [Any reason there is no DTS Disk Repository?](http://www.film-tech.com/vbb/forum/digital-cinema-forum/18542-any-reason-there-is-no-dts-disk-repository)
- (2022-02-08) [Recent films with DTS/Datasat](http://www.film-tech.com/vbb/forum/digital-cinema-forum/17953-recent-films-with-dts-datasat)
- (2021-12-30) [DTS playback with non-DTS hardware](http://www.film-tech.com/vbb/forum/digital-cinema-forum/16764-dts-playback-with-non-dts-hardware)
- (2021-10-10) [35 and 70 mm licorice pizza](http://www.film-tech.com/vbb/forum/digital-cinema-forum/14760-35-and-70-mm-licorice-pizza)
- (2020-06-29) [DTS TCR/ROM Questions](http://www.film-tech.com/vbb/forum/digital-cinema-forum/3973-dts-tcr-rom-questions)
- (2020-02-20) [Coping DTS audio files from a DTS player](http://film-tech.com/vbb/forum/digital-cinema-forum/1114-coping-dts-audio-files-from-a-dts-player)
- (2019-01-12) [DTS Disks hack](http://www.film-tech.com/ubb/f1/t012390.html)
- (2018-03-26) [What is DTS CD track order for 8-track *.AUD file?](http://www.film-tech.com/ubb/f1/t012286.html)
- (2017-10-15) [XD10 w/SMPTE timecode](http://www.film-tech.com/ubb/f1/t012210.html)
- (2016-07-29) [DAC decoder(s) in DTS-6D](http://www.film-tech.com/ubb/f1/t012031.html)
- (2015-04-20) [APX files on DTS disc?](http://www.film-tech.com/ubb/f1/t011814.html)
- (2004-06-12) [APT X-100 Encoding](http://www.film-tech.com/ubb/f1/t006266.html)
- (2004-03-22) [DTS to use Lossless encoding for cinema audio](http://www.film-tech.com/ubb/f1/t005983.html)
- (2003-07-30) [Fun things to do with a DTS DS3 disc](http://www.film-tech.com/ubb/f1/t005157.html)
- (2001-04-03) [DTS trailer files - can they be copied to another DTS disk?](http://www.film-tech.com/cgi-bin/ubb/f1/t002111.html)
  
