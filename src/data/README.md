# Official Dataset README

> online version: [https://gist.github.com/istar0me/4e098b7a0c3ba6177e6f06f7df5261d3](https://gist.github.com/istar0me/4e098b7a0c3ba6177e6f06f7df5261d3)
> 
- Before start training, we recommend you to read this documentation.
- Not only understand the dataset better, but also ensure all the files aren't loss or damaged.

## Outline

- [README](#readme)
  - [Outline](#outline)
  - [Dataset Information](#dataset-information)
    - [File Structure](#file-structure)
    - [`label.csv` Structure](#labelcsv-structure)
    - [Other](#other)
  - [Decompress Zip File](#decompress-zip-file)
    - [How to Decompress Zip File?](#how-to-decompress-zip-file)
  - [Check Zip File SHA256 Checksum](#check-zip-file-sha256-checksum)
    - [How to Get The SHA256 Checksum?](#how-to-get-the-sha256-checksum)
  - [Check The Number of Photos](#check-the-number-of-photos)
    - [How to Check The Number of Photos?](#how-to-check-the-number-of-photos)

## Dataset Information

### File Structure

```
.
├── orchid_training_set
│   ├── label.csv
│   ├── *.jpg
│   │   
│   │   ...
│   │   
│   └── *.jpg
├── orchid_public_set
│   ├── *.jpg
│   │   
│   │   ...
│   │   
│   └── *.jpg
└── orchid_private_set
    ├── *.jpg
    │   
    │   ...
    │   
    └── *.jpg
```

### `label.csv` Structure

```csv
filename,category
me3uqlixjn.jpg,0
5c0vsrdtpq.jpg,0
swixut5b3l.jpg,0
m0eqa926lo.jpg,0
5jr6x2y9p8.jpg,0
9y7sv8xqc2.jpg,0
nzt9hr5se2.jpg,0
niky1zwp74.jpg,0
3jdlrqgcz4.jpg,0
m4dtjfyu0w.jpg,0
utg5o0ih6z.jpg,1
lqm4f15bdw.jpg,1
h8q6mjt0kd.jpg,1
s63th18doy.jpg,1
gr8hxnsmju.jpg,1
...
```

- filename`<str>` : as it name implies, it's the filename in the directory.
- category`<int>` : the category(class) of the corresponding photo.
  - training set: from 0 to 218
  - public/private set: from 0 to **219**

### `train.csv`

- 將 `label.csv` 預先以 80%、20% 的比例切分為訓練（train）與驗證（valid）資料集的標籤檔
- 資料總共 2190 筆
- 切分資料時有考慮 `category` 的分布

### Other

- All the photos end with `.jpg`, there's no other format
- Photos only have two type of resolution: `(640x480)` and `(480x640)`

## Decompress Zip File

### How to Decompress Zip File?

1. Windows

   - Windows has built-in unzip feature, we suggest you using GUI, and double-click zip file to unzip.

2. Linux / MacOS

   1. Open Terminal, install `unzip` module
      
      ```shell
      $ sudo apt-get install -y unzip # for Ubuntu
      $ sudo yum install -y unzip     # for CentOS
      $ sudo brew install -y unzip    # for MacOS
      ```

   2. type `unzip -P <password> <zip_file>`, e.g.

      ```shell
      $ unzip -P '<password>' orchid_training_set.zip -d ./orchid_training_set
      $ unzip -P '<password>' orchid_public_set.zip -d ./orchid_public_set
      $ unzip -P '<password>' orchid_private_set.zip -d ./orchid_private_set
      ```

    * `-d` option specifies directory to which to extract files.
    * In case the password may contains special characters, please add `'`(single quote) next to password.

      ```shell
      # Example
      unzip -P !@#$%^&*() ... # incorrect, without single quote(')
      unzip -P "!@#$%^&*()" ... # incorrect, don't use double quote(")
      unzip -P '!@#$%^&*()' ... # correct
      ```
  

## Check Zip File SHA256 Checksum

- Purpose: Prevent zip file corrupted

```
orchid_training_set.zip:
783bb1c0eca98b5fb63049b33f6b908d670bf8ed79e576efd7e40810bb854a81

orchid_public_set.zip:
fbf777dcfd3041478033e3369d4dcbfbd751e4b0837c962d3c222f42095af5d0

orchid_private_set.zip:
62998d82fc2ce0422011c0af24892dba990ba21f928e662d381906e7a5942cb3
```

### How to Get The SHA256 Checksum?

1. Windows

   - Open Command Line(CMD), and type `certutil -hashfile <file> SHA256`, e.g.

      ```cmd
      C:\>certutil -hashfile orchid_training_set.zip SHA256
      C:\>certutil -hashfile orchid_public_set.zip SHA256
      C:\>certutil -hashfile orchid_private_set.zip SHA256
      ```

2. Linux

   - Open Terminal, and type `sha256sum <file>`, e.g.

      ```shell
      $ sha256sum orchid_training_set.zip
      $ sha256sum orchid_public_set.zip
      $ sha256sum orchid_private_set.zip
      ```

   - There's a more straight-forward method, it'll indicate whether match or not

      ```shell
      $ echo "783bb1c0eca98b5fb63049b33f6b908d670bf8ed79e576efd7e40810bb854a81 orchid_training_set.zip" | sha256sum -c
      $ echo "fbf777dcfd3041478033e3369d4dcbfbd751e4b0837c962d3c222f42095af5d0 orchid_public_set.zip" | sha256sum -c
      $ echo "62998d82fc2ce0422011c0af24892dba990ba21f928e662d381906e7a5942cb3 orchid_private_set.zip" | sha256sum -c

      # output
      orchid_training_set.zip: OK
      orchid_public_set.zip: OK
      orchid_private_set.zip: OK
      ```

3. MacOS

   - Open Terminal, and type `shasum -a 256 <file>`, e.g.

      ```shell
      $ shasum -a 256 orchid_training_set.zip
      $ shasum -a 256 orchid_public_set.zip
      $ shasum -a 256 orchid_private_set.zip
      ```

   - There's another method, it'll highlight checksum when it matchs

      ```shell
      $ shasum -a 256 orchid_training_set.zip | grep 783bb1c0eca98b5fb63049b33f6b908d670bf8ed79e576efd7e40810bb854a81
      $ shasum -a 256 orchid_public_set.zip | grep fbf777dcfd3041478033e3369d4dcbfbd751e4b0837c962d3c222f42095af5d0
      $ shasum -a 256 orchid_private_set.zip | grep 62998d82fc2ce0422011c0af24892dba990ba21f928e662d381906e7a5942cb3
      ```

## Check The Number of Photos

- The number of photos
  - Training Set: 2,190 photos
  - Public Set: 40,285 photos
  - Private Set: 41,425 photos

### How to Check The Number of Photos?

1. Windows

    1. [Decompress the dataset](#how-to-decompress-zip-file)
    2. Open Command Line(CMD) in the decompressed folder, and type `forfiles /m *jpg  | find "jpg" /c /i`

    - Example:

      ```cmd
      C:\orchid_training_set>forfiles /m *jpg  | find "jpg" /c /i
      2190
      ```

2. Linux / MacOS

    1. [Decompress the dataset](#how-to-decompress-zip-file)
    2. Open Terminal in the decompressed folder, and type `find . -name '*.jpg' | wc -l`

    - Example:
    
      ```shell
      ~/orchid_training_set$ find . -name '*.jpg' | wc -l
      2190
      ```