# How to backup Raspian

There's a good resource [here](https://blog.jaimyn.dev/the-fastest-way-to-clone-sd-card-macos/).


## Create image from SD Card

1. Use `diskutil list` to determine which disk (SSD) to backup:

```zsh
$ diskutil list
/dev/disk0 (internal, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *500.3 GB   disk0
   1:                        EFI ⁨EFI⁩                     314.6 MB   disk0s1
   2:                 Apple_APFS ⁨Container disk1⁩         500.0 GB   disk0s2

/dev/disk1 (synthesized):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      APFS Container Scheme -                      +500.0 GB   disk1
                                 Physical Store disk0s2
   1:                APFS Volume ⁨Macintosh HD - Data⁩     223.3 GB   disk1s1
   2:                APFS Volume ⁨Preboot⁩                 433.4 MB   disk1s2
   3:                APFS Volume ⁨Recovery⁩                613.9 MB   disk1s3
   4:                APFS Volume ⁨VM⁩                      2.1 GB     disk1s4
   5:                APFS Volume ⁨Macintosh HD⁩            15.1 GB    disk1s5
   6:              APFS Snapshot ⁨com.apple.os.update-...⁩ 15.1 GB    disk1s5s1

/dev/disk2 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *32.0 GB    disk2
   1:             Windows_FAT_16 ⁨RECOVERY⁩                2.6 GB     disk2s1
   2:                      Linux ⁨⁩                        33.6 MB    disk2s5
   3:             Windows_FAT_32 ⁨boot⁩                    268.4 MB   disk2s6
   4:                      Linux ⁨⁩                        29.1 GB    disk2s7
```

2. Execute the following where the disk is corollary to the disk you foun din the previous step:

```zsh
$ sudo gdd if=/dev/disk2 of=pi_backup.dmg status=progress bs=16M
```

## Write an image to an SD card.

Assuming you have an image named `pi_backup.dmg` and you want to write to the disk associated with `/dev/disk2`, execute the following:

```zsh
$ sudo gdd of=/dev/disk2 if=pi_backup.dmg status=progress bs=16M
```

