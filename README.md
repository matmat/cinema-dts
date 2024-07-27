# cinema-dts

## .AUD/.AUE File format
|Offset||Field|Format|Length|
|-|-|-|-|-|
|0x00|0|Film name|zstr|60|
|0x3c|60|Language|zstr|8|
|0x44|68|Studio|zstr|7|
|0x4b|75|Optical fall-back format|uint16_le|2|
|0x4e|78|Reel number|uint16_le|2|
|0x50|80|Serial number|uint16_le|2|
|0x5c|92|Encrypted flag|uint8|1|
|0x5d|93|AUE encryption key|uint16_le|2|

### Reel number
13 = Trailer, iff Serial number equals 1253
14 = Trailer
15 = Trailer, iff Serial number equals 1004
Everything else is a Feauture
