The MIF format is used in themes for Symbian, and also probably in arbitrary applications to pack and access resources.

There had been a (proprietary?) mifconv.exe utility in some SDK.

Sample file: https://www.deviantart.com/eggy/art/Ayofe-Theme-for-Symbian-S60v3-58630819 (extract it from .sis e.g. with SISContents).

##### Analysis

The file starts with a `B##4` entry and has many `C##4` entries. 4-byte big-endian integers are used for entry values.

All entries in the sample file (both `B##4` and `C##4`) have `0x01000000` and `0x20000000` fields after the header.

`B##4` then has `0xfa040000` (number of 8-byte entries). Each entry is a pair of duplicated addresses of `C##4` entries, 4+4 bytes. The order of addresses is not sequential.

`C##4` then has a number of bytes in data entry, some other fields:

* `0x01000000`
* `0x07000000`
* `0x00000000`
* `0x04000000`
* the data themselves finally.

Most `C##4` entries end with a `0xe803fefefeff` marker, but some end with a truncated `0xe803fefeff` one (included into the entry length).
