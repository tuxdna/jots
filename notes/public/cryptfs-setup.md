Creating a portable encrypted disk

    $ cd /data/dev/tmp/
    $ mkdir encrpyt 
    $ cd encrpyt/
    $ dd if=/dev/zero of=cryptfile bs=1M count=500
    500+0 records in
    500+0 records out
    524288000 bytes (524 MB) copied, 1.39907 s, 375 MB/s
    $ sudo losetup /dev/loop0 cryptfile 
    $ sudo badblocks -s -w -t random -v /dev/loop0
    Checking for bad blocks in read-write mode
    From block 0 to 511999
    Testing with random pattern: done                                
    Reading and comparing: done                                
    Pass completed, 0 bad blocks found.
    $ sudo modprobe blowfish
    $ sudo cryptsetup -y luksFormat -c blowfish -s 256 /dev/loop0
        
    WARNING!
    This will overwrite data on /dev/loop0 irrevocably.
    
    Are you sure? (Type uppercase yes): YES
    Enter LUKS passphrase: 
    Verify passphrase: 
    
    $ sudo cryptsetup luksOpen /dev/loop1 crypt_fun
    
    $ sudo mkfs.ext3 -j /dev/mapper/crypt_fun
    mke2fs 1.41.14 (22-Dec-2010)
    Filesystem label=
    OS type: Linux
    Block size=1024 (log=0)
    Fragment size=1024 (log=0)
    Stride=0 blocks, Stripe width=0 blocks
    127512 inodes, 509952 blocks
    25497 blocks (5.00%) reserved for the super user
    First data block=1
    Maximum filesystem blocks=67633152
    63 block groups
    8192 blocks per group, 8192 fragments per group
    2024 inodes per group
    Superblock backups stored on blocks: 
    	8193, 24577, 40961, 57345, 73729, 204801, 221185, 401409
    
    Writing inode tables: done                            
    Creating journal (8192 blocks): done
    Writing superblocks and filesystem accounting information: done
    
    This filesystem will be automatically checked every 20 mounts or
    180 days, whichever comes first.  Use tune2fs -c or -i to override.
    
    $ sudo e2fsck -f /dev/mapper/crypt_fun
    e2fsck 1.41.14 (22-Dec-2010)
    Pass 1: Checking inodes, blocks, and sizes
    Pass 2: Checking directory structure
    Pass 3: Checking directory connectivity
    Pass 4: Checking reference counts
    Pass 5: Checking group summary information
    /dev/mapper/crypt_fun: 11/127512 files (0.0% non-contiguous), 26636/509952 blocks
    
    $ mkdir my_crypt_fs
    $ sudo mount /dev/mapper/crypt_fun ./my_crypt_fs
    
Scripts

    File: mountCrypt.sh
    ===============================
    #! /bin/sh
    (losetup /dev/loop0 /home/you/cryptfile || echo) && (cryptsetup luksOpen /dev/loop0 crypt_fun && mount /dev/mapper/crypt_fun /media/fun)
    ===============================
    

    File: umountCrypt.sh
    ===============================
    #! /bin/sh
    umount /media/fun && cryptsetup luksClose crypt_fun && losetup -d /dev/loop0 
    ===============================
    

## Reference
 * http://goohackle.com/how-to-create-a-portable-encrypted-file_system-on-a-loop-file/

