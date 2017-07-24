******************************************************
Working with persistent storage: volumes and snapshots
******************************************************

Volumes are basically UNIX disks ("block devices") that will persist
after you terminate your instance.  They are tied to a zone within a
region and can only be mounted on instances within that zone.

Snapshots are an Amazon-specific thing that let you communicate data
on volumes between accounts.  They are "read-only" backups that are
created from volumes; they can be used to create new volumes in turn,
and can also be shared with specific people (or made public).
Snapshots are tied to a region but not a zone.

Creating persistent volumes to store data
=========================================

0. Locate your instance *zone*
------------------------------

.. image:: ../images/add-volume-1d.png
   :width: 80%

1. Click on the volumes tab
---------------------------

.. image:: ../images/add-volume-1.png
   :width: 80%

2. 'Create Volume'
------------------

.. image:: ../images/add-volume-1b.png
   :width: 80%

3. Configure your volume to have the same zone as your instance
---------------------------------------------------------------

.. image:: ../images/add-volume-1c.png
   :width: 80%

4. Wait for your volume to be available
---------------------------------------

.. image:: ../images/add-volume-2.png
   :width: 80%

5. Select volume, Actions, Attach volume
----------------------------------------

.. image:: ../images/add-volume-3.png
   :width: 80%

6. Select instance, attachment point, and Attach
------------------------------------------------

Here, your attachment point will be '/dev/sdf' and your block device will
be named '/dev/xvdf'.

.. image:: ../images/add-volume-4.png
   :width: 80%

7. On your instance, list block devices
---------------------------------------

Type::

   lsblk

You should see something like this::

  NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
  xvda    802:0    0    8G  0 disk
  `-xvda1 802:1    0    8G  0 part /
  xvdf    802:80   0  100G  0 disk

Now format the disk (ONLY ON EMPTY DISKS - THIS WILL ERASE ANY DATA ON
THE DISK)::

   sudo mkfs -t ext4 /dev/xvdf

and mount the disk::

   sudo mkdir /disk
   sudo mount /dev/xvdf /disk
   sudo chmod a+rwxt /disk

and voila, anything you put on /disk will be on the volume that you allocated!

The command 'df -h' will show you what disks are actually mounted & where.

Detaching volumes
-----------------

1. Unmount it from the instance
-------------------------------

Change out of the directory, stop any running programs using it, and then::

  sudo umount /disk

2. Detach
---------

On the 'volumes' tab in your EC2 console, go to Actions, Detach.

.. image:: ../images/add-volume-5.png
   :width: 80%

3. Yes, detach.
---------------

.. image:: ../images/add-volume-6.png
   :width: 80%

Note, volumes remain attached when you reboot or stop an instance, but
are (of course) detached when you terminate an instance.

Creating snapshots of volumes
=============================

1. Actions, Create snapshot
---------------------------

.. image:: ../images/create-snapshot-1.png
   :width: 80%

2. Fill out name and description
--------------------------------

.. image:: ../images/create-snapshot-2.png
   :width: 80%

3. Click 'Close' & wait.
------------------------

.. image:: ../images/create-snapshot-3.png
   :width: 80%
