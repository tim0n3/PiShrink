# PiShrink README

## Overview

The `PiShrink` bash script is designed to shrink Raspberry Pi disk images to a smaller size, helping you save space and make it easier to share or clone your Raspberry Pi SD card. It works by resizing the filesystem to its minimum size and then truncating the image file accordingly. You can also choose to compress the shrunken image using gzip or xz, and even enable parallel compression for improved performance.

## Version

Current version: v0.1.3

## Prerequisites

To use `PiShrink`, you need to have the following tools installed on your system:

- `parted`
- `losetup`
- `tune2fs`
- `md5sum`
- `e2fsck`
- `resize2fs`

Additionally, you may choose to use parallel compression, which requires `pigz` for gzip compression or `xz` for xz compression. Make sure these tools are available on your system if you intend to use them.

## Usage

Run `PiShrink` with the following command:

```bash
./PiShrink.sh [-adhrsvzZ] imagefile.img [newimagefile.img]
```

### Options

- `-a`: Compress the image in parallel using multiple CPU cores.
- `-d`: Write debug messages in a debug log file.
- `-h`: Show the help message with usage information.
- `-r`: Use advanced filesystem repair options if the normal one fails.
- `-s`: Don't expand the filesystem when the image is booted for the first time.
- `-v`: Be verbose in the output.
- `-z`: Compress the shrunken image using gzip.
- `-Z`: Compress the shrunken image using xz.

### Arguments

- `imagefile.img`: The path to the input Raspberry Pi disk image that you want to shrink.
- `newimagefile.img`: (Optional) The path to the new image file where the shrunken image will be saved. If not provided, the original image will be overwritten.

## How It Works

1. `PiShrink` will check if the required tools are installed and whether you have the necessary privileges to run the script.

2. The script gathers information about the input image, such as its size and partition data.

3. If you choose to auto-expand the filesystem on boot, `PiShrink` will set up the necessary configurations.

4. It checks the filesystem for errors and attempts to repair it if any issues are found.

5. `PiShrink` shrinks the filesystem to its minimum size.

6. The script then shrinks the partition and truncates the image file accordingly.

7. Optionally, you can choose to compress the shrunken image using gzip or xz, with the option for parallel compression.

8. The shrunken or compressed image is saved as `newimagefile.img` or overwrites the original image.

## Note

- Be cautious when using the `-r` option for advanced filesystem repair, as it may not always be successful and could result in data loss.
- The `-s` option skips the auto-expanding process, which is useful for some Raspberry Pi images but not supported for all.
- Using the `-d` option enables debug mode, which logs additional information to a debug log file.

## Installation ##

```bash
wget https://raw.githubusercontent.com/Drewsif/PiShrink/master/pishrink.sh
chmod +x pishrink.sh
sudo mv pishrink.sh /usr/local/bin
```

## Example

Shrink a Raspberry Pi disk image and compress it using gzip:

```bash
./PiShrink.sh -z imagefile.img
```

```bash
[user@localhost PiShrink]$ sudo pishrink.sh pi.img
e2fsck 1.42.9 (28-Dec-2013)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/loop1: 88262/1929536 files (0.2% non-contiguous), 842728/7717632 blocks
resize2fs 1.42.9 (28-Dec-2013)
resize2fs 1.42.9 (28-Dec-2013)
Resizing the filesystem on /dev/loop1 to 773603 (4k) blocks.
Begin pass 2 (max = 100387)
Relocating blocks             XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
Begin pass 3 (max = 236)
Scanning inode table          XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
Begin pass 4 (max = 7348)
Updating inode references     XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
The filesystem on /dev/loop1 is now 773603 blocks long.

Shrunk pi.img from 30G to 3.1G
```

## Contributing ##

If you find a bug please create an issue for it. If you would like a new feature added, you can create an issue for it but I can't promise that I will get to it.

Pull requests for new features and bug fixes are more than welcome!

## License

This script is provided under an open-source license. Please review the [LICENSE](LICENSE) file for details.

## Author

`PiShrink` was created by [@Drewsif](https://github.com/Drewsif) and is maintained by [Drew Bonasera](https://github.com/Drewsif).

For any issues or questions, please refer to the [Issues](https://github.com/Drewsif/PiShrink/issues) or contact the maintainers.

Enjoy using `PiShrink` to efficiently manage your Raspberry Pi disk images!
