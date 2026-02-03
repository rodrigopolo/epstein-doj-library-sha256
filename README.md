# Epstein Library SHA256 Hashes

This repository only contains the SHA256 hashes of the files provided by the DOJ, original DOJ files can be downloaded from the official DOJ site:

* https://www.justice.gov/epstein/
* https://www.justice.gov/epstein/doj-disclosures

Direct links to ZIP files:
* Vol 01 https://www.justice.gov/epstein/files/DataSet%201.zip
* Vol 02 https://www.justice.gov/epstein/files/DataSet%202.zip
* Vol 03 https://www.justice.gov/epstein/files/DataSet%203.zip
* Vol 04 https://www.justice.gov/epstein/files/DataSet%204.zip
* Vol 05 https://www.justice.gov/epstein/files/DataSet%205.zip
* Vol 06 https://www.justice.gov/epstein/files/DataSet%206.zip
* Vol 07 https://www.justice.gov/epstein/files/DataSet%207.zip
* Vol 10 `magnet:?xt=urn:btih:d509cc4ca1a415a9ba3b6cb920f67c44aed7fe1f&dn=DataSet%2010.zip`
* Vol 12 https://www.justice.gov/epstein/files/DataSet%2012.zip

### Vol 1
Available by direct link https://www.justice.gov/epstein/files/DataSet%201.zip `DataSet 1.zip` SHA256 `598f4d2d71f0d183cf898cd9d6fb8ec1f6161e0e71d8c37897936aef75f860b4` with a total size of 1,321,480,300 bytes, it contains 3,158 files:

* 1 `DAT` file
* 1 `OPT` file
* 3156 `pdf` files

Hashes available in `VOL00001.txt`

### Vol 2
Available by direct link https://www.justice.gov/epstein/files/DataSet%202.zip `DataSet 2.zip` SHA256 `24cebbaefe9d49bca57726b5a4b531ff20e6a97c370ba87a7593dd8dbdb77bff` with a total size of 661,431,549 bytes, it contains 577 files:

* 1 `avi`
* 1 `DAT`
* 1 `OPT`
* 574 `pdf`

Hashes available in `VOL00002.txt`

### Vol 3
Available by direct link https://www.justice.gov/epstein/files/DataSet%203.zip `DataSet 3.zip` SHA256 `1c5587152328bd45a68baefeb5fba1d55677be4ff0b381d721f37c7b3da9055e` with a total size of 623,898,185 bytes, it contains 69 files:

* 1 `DAT`
* 1 `OPT`
* 67 `pdf`

Hashes available in `VOL00003.txt`

### Vol 4
Available by direct link https://www.justice.gov/epstein/files/DataSet%204.zip `DataSet 4.zip` SHA256 `979154842bac356ef36bb2d0e72f78e0f6b771d79e02dd6934cff699944e2b71` with a total size of 368,592,729 bytes, it contains 154 files:

* 1 `DAT`
* 1 `OPT`
* 152 `pdf`

Hashes available in `VOL00004.txt`

### Vol 5
Available by direct link https://www.justice.gov/epstein/files/DataSet%205.zip `DataSet 5.zip` SHA256 `7317e2ad089c82a59378a9c038e964feab246be62ecc24663b741617af3da709` with a total size of 64,464,128 bytes, it contains 122 files:

* 1 `DAT`
* 1 `OPT`
* 120 `pdf`

Hashes available in `VOL00005.txt`

### Vol 6
Available by direct link https://www.justice.gov/epstein/files/DataSet%206.zip `DataSet 6.zip` SHA256 `d54d26d94127b9a277cf3f7d9eeaf9a7271f118757997edac3bc6e1039ed6555` with a total size of 53,775,966 bytes, it contains 15 files:

* 1 `DAT`
* 1 `OPT`
* 13 `pdf`

Hashes available in `VOL00006.txt`

### Vol 7
Available by direct link https://www.justice.gov/epstein/files/DataSet%207.zip `DataSet 7.zip` SHA256 `51e1961b3bcf18a21afd9bcf697fdb54dac97d1b64cf88297f4c5be268d26b8e` with a total size of 101,686,422 bytes, it contains 19 files:

* 1 `DAT`
* 1 `OPT`
* 17 `pdf`

Hashes available in `VOL00007.txt`

### Vol 10
Available by torrent, `DataSet 10.zip` SHA256 `7d6935b1c63ff2f6bcabdd024ebc2a770f90c43b0d57b646fa7cbd4c0abcf846` with a total size of 84,439,381,640 bytes, it contains 504,030 files:

* 1 `.3gp` file
* 1 `.DAT` file
* 1 `.OPT` file
* 1 `.mp3` file
* 1 `.pluginpayloadattachment` file
* 5 `.amr` files
* 5 `.wav` files
* 16 `.opus` files
* 17 `.m4a` files
* 25 `.m4v` files
* 154 `.mov` files
* 649 `.mp4` files
* 503154 `.pdf` files

Hashes available in `VOL00010.txt`

### Vol 12
Available by direct link https://www.justice.gov/epstein/files/DataSet%2012.zip `DataSet 12.zip` SHA256 `b5314b7efca98e25d8b35e4b7fac3ebb3ca2e6cfd0937aa2300ca8b71543bbe2` with a total size of 119,634,859 bytes, it contains 154 files:

* 1 `DAT`
* 1 `OPT`
* 152 `pdf`

Hashes available in `VOL00012.txt`

## SHA256 Script
This script generate the SHA256 hashes from the zip files using GNU utilities
```sh
#!/bin/bash

ZIP_FILE="$1"
OUTPUT="$2"

export ZIP_FILE

hash_file() {
    local file="$1"
    local hash=$(unzip -p "$ZIP_FILE" "$file" | shasum -a 256 | cut -d' ' -f1)
    echo "$hash  $file"
}

export -f hash_file

# Get list of files (exclude directories)
unzip -Z1 "$ZIP_FILE" | grep -v '/$' | \
    parallel -j 8 --progress --eta hash_file \
    > "$OUTPUT"
```
