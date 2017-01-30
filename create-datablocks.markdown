---
layout: default
---

# Adding a `CEPH` datablock to your Virtual Machine

We recommend you to run your operating system on a small `SSD image` and store your bulk data on `Ceph datablock`(s). 

In this page we will show you how to create `Ceph datablock`s of customisable size for your bulk data and make it available to your Virtual Machine.

The steps you require to add a `Ceph datablock` to your Virtual Machine are:

1. Create a new empty datadisk
2. Add the new datadisk to the template
3. Mount the datadisk in the VM

## Create a new empty datadisk

In this section we will be setting up an empty disk on [ceph Datastore](image_storage).

1. Login to the UI at the following URL: [https://ui.hpccloud.surfsara.nl](https://ui.hpccloud.surfsara.nl)
2. From the menu at the left pane, select the _Images_ page under _Storage_.
3. Click on the green [+] button on the top. A new window appears titled *Create image*.
4. Fill in the *Create image* form that popped up:
	* Name: give a name meaningful for your datablock, e.g. **output data**. You will use this name later in your `Template`.
	* Description (optional): give information about the datablock
    * Type: set to *Generic storage datablock*
    * Datastore: choose `111: ceph`
    * Check *This image is persistent* checkbox. If you omit this, your data will not be saved on the disk once you shutdown the VM. You can also change this flag later from the [image persistence](image_persistence) properties.
    * On the _Image location:_ group, choose radio button _Empty disk image_
    * Give it a _Size_ in MB that is meaningful to you (e.g. insert 10000 to create a 10GB disk)
![add_datablock](images/add_datablock.png)
5. Click the green button *Create* on the form, to submit it. 

>**NOTE:**
>
>A new image will show on the `Images` list, and it will keep in status LOCKED while it is being created. When it is created it will come to status READY. Then you *still* have to format and mount the disk.


## Add the new datadisk to the template

In order to let you VM know about the new datablock, you need to add it to your VM's `template` by [editing storage options](customize-vm-storage).

1. On the UI, from the menu at the left pane select the *VMs* page under *Templates*. 
2. Click on your template and then click on the green *Update* button.
3. Select the *Storage* tab from the menu bar.
4. Click on the _+_ button under `Disk 0` (that will make a new _Disk 1_), and then choose the **output data** `image` you created as a second `image`.
![template_add_datablock](images/template_add_datablock.png)
5. Click the green button *Update* on the top, to submit it.

>**NOTE:**
>
>The datablock will be available to your VM the next time you instantiate it. If your VM is running then changes in the Template will not have any effect.


## Mount the datadisk in the VM

In this section we show you how you can start using the new disk.

1. On the UI, from the menu at the left pane select the *VMs* page under *Instances*. Create a new `VM` by selecting the `Template` you created in the previous step. 
2. Once the `VM` is in RUNNING state, ssh as root to the machine using your SSH-key. 
3. Run `fdisk -l` and see that your new datablock is there (Disk /dev/vdb: 10.5 GB).
4. Mount the datadisk in the VM:

>**Warning:**
>
>In the following listing, the first `mkdir` and `mkfs` commands only need to be run once (and they do **destroy** everything on the image!). The `mount` command (fourth line) needs to be run every time you start the VM with that image. Alternatively, you can add this line to /etc/fstab to have it done automatically: `/dev/vdb /data xfs defaults 0 0`. 
>
>The last lines (the one with `mkdir -p` onwards) ask the operating system to perform some optimisations when using Ceph. Note that the directory /etc/rc.d/ may or may not exist, but the -p will make sure that it exists after the command is run.

```sh
sudo su -
mkdir /data  
mkfs -t xfs /dev/vdb  
mount /dev/vdb /data
mkdir -p /etc/rc.d/ && touch /etc/rc.d/rc.local
echo "echo 4096 > /sys/block/vdb/queue/read_ahead_kb" > /etc/rc.d/rc.local
chmod 755 /etc/rc.d/rc.local
```

