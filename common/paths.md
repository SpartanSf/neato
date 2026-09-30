# NEATO Paths Specification

Written by piguman3

Revision 2 of September 29, 2026

---

NEET Computers by default uses "partition:filepath" for most of its functions, but, to lower the number of arguments
and the complexity of many things in NEATO we instead have adopted the format of "disk:partition:filepath".

The `filepath` component is an absolute path from the root of the partition and always begins with `/`. A path that
ends in `/` refers to a directory.

The `disk` component may be the literal `any` instead of a disk number, meaning that the path may be resolved against
any disk (for example, `any:system:/boot/cfg/boot.lua` in the [bootloader specification](../boot/bootloader.md)).

---

### Examples

- `0:bios:/hello.lua` -> file named "hello.lua", at the root of partition "bios" on disk number 0.
- `4:hello:/my/epic/file.lua` -> file named "file.lua" inside of directory "epic", inside of "my", which is at the root
  of partition "hello" on disk number 4.
