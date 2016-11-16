disktype: Disk Format Detection
---------------------------------------------------------------------------------------------------

'''Important''': This is not the official disktype repository, nor does it track maintenance updates
to the official repository. Unless you are involved in a project that I'm currently working on, you
should go and get Christoph Pfisterer's official version at http://disktype.sourceforge.net/

I created this fork to simplify access to a patched, updated version of disktype for my own purposes. 
The current version of the fork applies the unattended-to Atari and BSD patches from the official respository,
adds ext4 support adapted from the patch at 

* https://github.com/Pardus-Linux/Packages/tree/master/system/base/disktype/files, 

and exfat support from the patch at 

* https://github.com/ericpaulbishop/gargoyle/tree/master/package/disktype/patches

Additional support for Expert Witness Format files based on existing (but non-functional) patch is
in progress in the dtewf branch.

# Introduction 

The purpose of disktype is to detect the content format of a disk or
disk image. It knows about common file systems, partition tables, and
boot codes.

The program is written in C and is designed to compile on any modern
Unix flavour. It is self-contained and in general works without
special libraries or headers. Some system-dependent features can be
used to gather additional information.


# Installation

GNU make is required to build disktype. The Makefile is set up to use
GCC, but disktype should compile with any C compiler. To change the
compiler, you can edit the Makefile or set the standard variables CC,
CPPFLAGS, CFLAGS, LDFLAGS, and LIBS from the make command line.

The Makefile uses uname to determine the system type and enables
certain system-dependent features based on that. If you run into
problems, you can disable all system-dependent features by setting the
variable NOSYS, as in 'make NOSYS=1'.

Running make in the src/ directory results in the binary 'disktype'. Copy it to a 'bin'
directory of your choice, optionally stripping it on the way. It does
not require any additional files.

The manual page 'disktype.1' can be copied to
/usr/local/share/man/man1 or a similar directory that is suitable for
your system and policy. If you package disktype for binary
distribution, please also include the README, HISTORY, TODO, and
LICENSE files in a place like /usr/share/doc/disktype.


# Usage

The 'disktype' program can be run with any number of regular files or
device special files as arguments. They will be analyzed in the order
given, and the results printed to standard output. There are no
switches in this version. Note that running disktype on device files
like your hard disk will likely require root rights.

See the online documentation at <http://disktype.sourceforge.net/doc/>
for some example command lines (or view the same pages offline in
the doc/ directory in this repository).


# Recognized Formats

The following formats are recognized by this version of disktype.

File systems: FAT12/FAT16/FAT32, ExFAT, NTFS, HPFS, MFS, HFS, HFS Plus,
  ISO9660, ext2/ext3/ext4, Minix, ReiserFS, Reiser4, Linux romfs, Linux
  cramfs, Linux squashfs, UFS (some variations), SysV FS (some
  variations), JFS, XFS, Amiga FS/FFS, Amiga SFS, Amiga PFS, BeOS BFS,
  QNX4 FS, UDF, 3DO CD-ROM file system, Veritas VxFS, Xbox DVD file
  system.

Partitioning: DOS/PC style, EFI GPT, Apple, Amiga "Rigid Disk", ATARI
  ST (AHDI3), BSD disklabel, Linux RAID physical disks, Linux LVM1
  physical volumes, Linux LVM2 physical volumes, Solaris x86 disklabel
  (vtoc), Solaris SPARC disklabel.

Other structures: Debian split floppy header, Linux swap.

Disk images: Raw CD image (.bin), Virtual PC hard disk image, Apple
  UDIF disk image (limited), Linux cloop (limited).

Boot loaders: LILO, GRUB, SYSLINUX, ISOLINUX, Linux kernel, FreeBSD
  loader, Windows/MS-DOS loader, BeOS loader, Haiku loader, Sega
  Dreamcast.

Compression formats: gzip, compress, bzip2.

Archive formats: tar, cpio, bar, dump/restore.


Compressed files (gzip, compress, bzip2 formats) will also have their
contents analyzed using transparent decompression. The appropriate
compression program must be installed on the system, i.e. 'gzip' for
the gzip and compress formats, 'bzip2' for the bzip2 format.

Disk images in general will also have their contents analyzed using
the proper mapping, with the exception of the Apple UDIF format.

See the online documentation at <http://disktype.sourceforge.net/doc/>
for more details on the supported formats and their quirks (or view the 
same pages offline in the doc/ directory in this repository).


# Maintenance and Planned Updates

This fork of disktype is intended to address ongoing community needs.
If you find a file system or disk image that it doesn't currently
cover, please add a comment as an "Issue" in this repository.

