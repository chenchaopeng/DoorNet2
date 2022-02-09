## 扩容rootfs流程
脚本执行  可用bash

``` 
cfdisk /dev/mmcblk0 

PART_START=$(fdisk -l | grep /dev/mmcblk0p2 | awk '{print $2}')
        fdisk /dev/mmcblk0 <<EOF
        P
        d
        2
        n
        p
        $PART_START
        
        n
        p
        w
EOF

resize2fs -p /dev/mmcblk0p2

sync

poweroff

```

建议创建脚本sh来执行