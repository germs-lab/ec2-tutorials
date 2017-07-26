***********************************
Running RStudio Server in the cloud
***********************************

In this section, we will run RStudio Server on a remote Amazon machine.
This will require starting up an instance, configuring its network firewall,
and installing and running some software.

.. @@remember to terminate
.. @@can we reboot and have it sart up again?
.. @@diagram laying out zone etc.

Reference documentation for running RStudio Server on Ubuntu:

   https://www.rstudio.com/products/rstudio/download-server/

-----

1. Start up an Amazon instance
------------------------------

Start an Ubuntu image using ami-05ed6813 on an m4.xlarge machine, as per the instructions here:

:doc:`boot`

2. Configure your network firewall
----------------------------------

Normally, Amazon computers only allow shell logins via ssh.
Since we want to run a Web service, we need to give the outside world
access to other network locations on the computer.

Follow these instructions:

:doc:`configure-firewall`

(You can do this while the computer is booting.)

You'll also want to update your DNS support and ensure that both DNS resolution and DNS hostnames are set to "yes" by following these `instructions. <http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-dns.html#vpc-dns-updating>`_

3. Log in via the shell
-----------------------

Follow these instructions to log in via the shell:

:doc:`login-shell`.


4. Install R and the RStudio tool
---------------------------------

Type the following commands ::

    sudo docker pull docker pull rocker/rstudio
    sudo docker run -d -p 8787:8787 rocker/rstudio

This will take a few minutes.

Upon success, you should see something a print out of alphanumerics.

5.  Download data for the visualization tutorial
------------------------------------------------

Get the data here ::

    cd /root/rstudio
    sudo wget https://raw.githubusercontent.com/data-lessons/gapminder-R/gh-pages/data/raw_data/gapminder.csv

6. Open your RStudio Server instance
------------------------------------

Finally, go to 'http://' + your IPv4 public hostname + ':8787' in a browser,
eg. ::

   http://XX.XXX.XXX.XXX:8787/

and log into RStudio with username 'rstudio' and the password 'rstudio'
you set it to above.

Voila!

----

You can now just go ahead and use this, or you can "stop" it, or you
can freeze into an AMI for later use.

Note that on reboot, RStudio Server will start up again and all your files
will be there.

Go back to the index: :doc:`index`.


.. @@ meditations on file transfer
