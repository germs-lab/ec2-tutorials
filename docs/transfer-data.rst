*********************************************************
Transfer data to and from an EC2 instance using Filezilla
*********************************************************

You will need the ``amazon-key.pem`` file that was downloaded in
step 11 of booting up your new instance (see :doc:`boot`).

Download Filezilla
==================

Download the FTP application `Filezilla <https://filezilla-project.org/>_`.  Note:  There is an optional step in my install that asked if I wanted Yahoo to be my default browser, and I checked "NO".

Open FileZilla
==============
Near the top of the screen, you will need to provide the following information:  Host, username, and port.  We will also need to provide a password which is associated with your *.pem EC2 key file.

Password:

To let Filezilla know where your key file is, you can assign it through the FileZilla --> Settings -->  SFTP --> Add key file --> Select your *pem file

Host:  

Your host name is the public DNS of your EC2 instance, e.g., ec2-52-32-45-44.us-west-2.compute.amazonaws.com

Username:

Your username is *ubuntu*

Port:

By default, the port for SFTP is *22*.

Once this is filled in, you can press the *Quickconnect* button and you will see files that are in your /home/ubuntu directory on your server.  You may now move files to and fro.

