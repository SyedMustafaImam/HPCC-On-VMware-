<div align="right">


<p style='color:#FAF9F6;font-size:32px; font-weight:bold'>Parallel &amp; Distributed Computing </p>


<p style='color:#FAF9F6;font-size:32px; font-weight:bold'>Final Project</p>


<p style='color:#FAF9F6;font-size:29px; font-weight:bold'> Topic: HPC Clusters</p>

<p style='color:#FAF9F6;font-size:21.4px; font-weight:bold'>Project Report</p>
<p style='color:#FAF9F6;font-size:15.1px; font-weight:bold'>Section: BSCS 7A</p>
<p style='color:#FAF9F6;font-size:15.1px; font-weight:bold'>By</p>
<p style='color:#FAF9F6;font-size:15.1px;'>
Syed Hurrar Hasan Rizvi (1812135)</p>
<p style='color:#FAF9F6;font-size:15.1px;'>
Syed Mustafa Imam (1812134)
</p>
<p style='color:#FAF9F6;font-size:15.1px;'>
Hirdesh Kumar (1812114)
</p>
<p style='color:#FAF9F6;font-size:15.1px;'>
Elliott Francis Joseph (1812110)
</p>
<p style='color:#FAF9F6;font-size:15.1px;'>
Date: 23-12-2021
</p>

</div> 

<p style='color:white;font-size:28px;font-weight:bold'>
Table of contents 
</p>

- [**1.Introduction**](#1introduction)
- [**2.Use Cases**](#2use-cases)
  - [**Research Labs**](#research-labs)
  - [**Media And Entertainment**](#media-and-entertainment)
  - [**Oil and gas**](#oil-and-gas)
  - [**Artificial Intelligence**](#artificial-intelligence)
  - [**Financial Services**](#financial-services)
- [**3.Steps:**](#3steps)
  - [**Creation Of Virtual Machines**](#creation-of-virtual-machines)
  - [**Linux Installation on nodes**](#linux-installation-on-nodes)
  - [**Configuring etc host file**](#configuring-etc-host-file)
  - [**SSH equivalence establishment for user root**](#ssh-equivalence-establishment-for-user-root)
  - [**Setup NTP Service**](#setup-ntp-service)
  - [**Installation of PDSH**](#installation-of-pdsh)
  - [**Setup NFS**](#setup-nfs)
  - [**Creation of ordinary user and also setup SSH equivalence**](#creation-of-ordinary-user-and-also-setup-ssh-equivalence)
  - [**Installation of prerequisites packages (GCC, G77, etc)**](#installation-of-prerequisites-packages-gcc-g77-etc)
  - [**Installation of MPI**](#installation-of-mpi)
  - [**Compiling Linpack**](#compiling-linpack)
  - [**Benchmarking**](#benchmarking)


# **1.Introduction**

An HPC cluster is a collection of hundreds or thousands of servers that are networked together, each server is known as a node. Each node in a cluster works in parallel with each other, boosting processing speed to deliver high-performance computing. HPC is appropriate for most small and medium-sized businesses since these nodes are very close together, this is the reason why it is called a cluster. All cluster nodes have the same components as a laptop or desktop such as the CPU, cores, memory, and disk space. The difference between personal computers and a cluster node is in quantity, quality, and power of the components. User login to the cluster head node is done by using the ssh program.


# **2.Use Cases**

An HPC is Deployed on-premises, at the edge, or in the cloud. HPC solutions are used for a variety of purposes across multiple industries.HPC is used to help scientists find sources of renewable energy, understand the evolution of our universe. Predict and track the storms, and create new materials.

## **Research Labs**

HPC is used to help scientists find sources of renewable energy, understand the evolution of our universe, predict and track storms and create new materials.

## **Media And Entertainment**

HPC is used to edit feature films, render mind-blowing special effects, and stream live events around the world.

## **Oil and gas**

HPC is used to more accurately identify where to drill for new wells and to help boost production from existing wells.

## **Artificial Intelligence**

HPC is used to detect credit card fraud, provide self-guided technical support, reach self-driving vehicles, and improve cancer screening techniques.

## **Financial Services**

HPC is used to track real-time stock trends and automate trading.


# **3.Steps:**

## **Creation Of Virtual Machines**

The master node is set up by the name &#39;HPC Master&#39; with Red Hat Enterprise Linux 32 bit as the main OS of the Virtual Machine and the network working on a bridge network. The System Configuration of the HPC Master is presented below:

![ScreenShot](./Pictures/master.JPG)


The compute node is also created by the name &#39;node1&#39; with Red Hat Enterprise Linux 32 bit as the main OS of the Virtual Machine with a standard data store and a bridged network. The System Configuration of the HPCNode1 are presented below:

![ScreenShot](./Pictures/node1.JPG)


Another compute node is also created by the name &#39;node2&#39; with Red Hat Enterprise Linux 32 bit as the main OS of the Virtual Machine with a standard data store and a bridged network. The System Configuration of the HPCNode2 are presented below:

![ScreenShot](./Pictures/node2.JPG)


An NTP server was also created by using a node that is not part computation performed by a cluster. It was done by using Ubuntu OS 64 bit as the main OS of the Virtual Machine with a standard data store and a NAT network. System Configurations are presented below:

![ScreenShot](./Pictures/ntp.JPG)
## **Linux Installation on nodes**

After booting up from the image it will automatically go into the install mode.

Once it asks for input, press skip for skipping the media check.

Create a custom layout then add a partition with file type **swap** and size of **128MB** and additional size options as **fixed size** , then press ok.

Repeat the process one more time to create another partition with **ext3** file type and size of **128MB** and additional size options as **fixed to maximum allowable size** , then press ok.

Once we have a disk that is all you need. Just press Next then again next. It&#39;s going to have the hostname manually as the **master node,** then press edit above and uncheck **Enable IPv6 support** change dynamic IP to manual IP as **10.0.0.20** and prefix/netmask as **255.255.255.0** then press okay then press next then again next then continue as We don&#39;t want any gateway no DNS and let&#39;s specify our timezone, press next, again Press Next.

Specify the password as red hat then press next.

Uncheck desktop and Just click customize now. And now select packages from here. We don&#39;t want a desktop. We want **editors** , **development libraries, and development tools** I won&#39;t have to use. Go to the base system. uncheck **dial network support**.

So that is all you will need right now. so just go to next. Press Next to start the installation and so on, we will be done.

Once the system is completely installed, select reboot.

Remember that your nodes in your HPC cluster should be of the same hardware, same processor architecture, and the same version of the operating system you&#39;re using.

Let your system boot up. So this is how you would install Linux.

On a virtual machine now we&#39;ve two more nodes to go on which we need to install the Linux operating system. Once I&#39;m happy with the configuration of the system, we will copy the files from the backend. This is because we have here this version of VMware server that does not support cloning. So what we will be doing is shutting down this server/system/VM, and now copying its file disk file. As your server is turned off, let&#39;s go to the backend.

**Command:** cd machines

**Command:** ls

And we have this HPC master directory, which we have these files.

Let&#39;s enter into this directory by

**Command:** cd HPCMaster

**Command:** ls

**Command:** ls -lh

As you can see, this is your virtual machine disk file named **HPCMaster.vmdk** , which consumes 1.6 GB.

So now I&#39;m copying this file.

**Command:** ls ../Pictures/HPCNode1/

**Command:** ls ../Pictures/HPCNode1/ -lh

As you can see you have four files there. Now we will copy this VMDK file from here and overwrite this VMDK file here.

**Command:** cp HPCMaster.vmdk ../Pictures/HPCNode1/HPCNode1.vmdk

Press y for yes overwriting.

As you can see the file is copied so let&#39;s check the list.

**Command:** ls ../Pictures/HPCNode1/ -lh

Let&#39;s try starting node1 and see what happens. Click power on and go to the console window and let it boot up. It will have all settings from your HPC master. That means it will also have the same hostname, same IP everything.

Once this is booted up. So let&#39;s go to the console, it will seem like a master node, but it is not it is, as you can see here, this is **HPCNode1** and in the same way, we&#39;ll do the second node as well. But first, adjust the hostnames.

**Command:** vi /etc/sysconfig/network

Then edit hostname as **Node1**

And the IP is going to be

**Command:** vi /etc/sysconfig/network-scripts/ifcfg-eth0

Life config Ethernet zero should not get its IP from DHCP. It&#39;s going to be a static IP address equal to 10.0.0.11 and netmask is equal to 255.255.255.0

One more thing to see hosts.

**Command:** vi /etc/hosts

remove this master node at all from the script.

Now let&#39;s change the hostname manually.

**Command:** hostname node1

**Command:** service syslog restart

**Command:** less /var/log/messages

That will make sure that the logs in the various log messages are written correctly.

Press **shift G** you can see as soon as you&#39;ve restarted Syslog the logs here it says node1 now before it was master node.

Then reboot this system

**Command:** reboot

Now repeat the same process for Node2 as you have done for the Node1.

## **Configuring etc host file**

**Command:** vi /etc/hosts

Now delete IP version 6 naming file

Then remove a master node from this localhost line

Add three lines here

10.0.0.20 master node

10.0.0.11 node1

10.0.0.12 node2

Then back to the console.

**Command:**
```console
[node1@node1]# scp /etc/hosts node1:/etc/ 
```

Except for the fingerprint of node1, node1&#39;s password is redhat.

Do the same thing for node2

**Command:** 

```console
[node1@node1]# scp /etc/hosts node2:/etc/
```

Except for the fingerprint of node2, node2&#39;s password is redhat.

Now, the, etc hosts file is configured.

## **SSH equivalence establishment for user root**

Now we will generate public and private keys (DSA and RSA) of all nodes.

Generate dsa keys

**Command:** 
```console
ssh-keygen -t dsa
```
Just press enter, no need to enter a passphrase.

Now generate the rsa keys

**Command:** 
```console
ssh-keygen -t dsa
```

Just press enter, no need to enter a passphrase.

Now if you want you can check these keys

**Command:** 
```console
cd .ssh/
```
**Command:** 
```console
ls -l
```
As you can see both dsa and rsa are visible along with the public and private keys.

Now copy all four key files for this directory

**Command:** 
```console
cd ..
```
**Command:** 
```console
scp -r .ssh node1:/root/
```
Enter the password which is redhat

As files are copied in node 1 now do the same process for node 2.

**Command:** 
```console
scp -r .ssh node2:/root/
```

Now do one more step

**Command:**
```console
cd .ssh/
```

**Command:** 
```console
cat \*.pub \&gt;\&gt; authorized\_keys
```

**Command:** 
```console
cd ..
```

Now copy these files on both nodes again

**Command:** 
```console
scp -r .ssh node1:/root/
```

Enter the password which is redhat

As files are copied in node 1 now do the same process for node 2.

**Command:** 
```console
scp -r .ssh node2:/root/
```

Now We will generate RSA fingerprints,

**Command:**
```console
ssh-keyscan -t dsa masternode node1 node2
```

Now I&#39;m going to put it in a special file on this log

**Command:**
```console
ssh-keyscan -t dsa masternode node1 node2 \&gt; /etc/ssh/ssh\_known\_hosts
```

You see this file. This file is a valid one, but it does not exist by default. Now what I&#39;m going to do is I&#39;m going to scan the RSA keys of the same nodes and I&#39;m going to append that to this file.

**Command:** 
```console
ssh-keyscan -t rsa masternode node1 node2 \&gt;\&gt; /etc/ssh/ssh\_known\_hosts
```

Now see how the file looks like

**Command:** 
```console
less /etc/ssh/ssh\_known\_hosts
```

Now replicate this file to all nodes.

**Command:**
```console
scp /etc/ssh/ssh\_known\_hosts node1:/etc/ssh
```

**Command:**
```console
scp /etc/ssh/ssh\_known\_hosts node2:/etc/ssh
```
**Testing by logging it into each node**

**Command:**
```console
ssh masternode
```

**Command:**
```console
exit
```

**Command:**
```console
ssh node1
```
**Command:** 
```console
exit
```

**Command:**
```console
ssh node2
```
**Command:** 
```console
exit
```

**Testing by logging all nodes into each other node**

**Command:** 
```console
ssh masternode uptime
```
**Command:** 
```console
exit
```
**Command:** 
```console
ssh node1 uptime
```
**Command:**
```console
exit
```

**Command:** 
```console
ssh node2 uptime
```
**Command:** 
```console
exit
```
## **Setup NTP Service**

**Setupping NTP service on node1.**

**Command:** 
```console
vi /etc/ntp.conf
```
Disable server 0, server 1, server 2

Disable server local-clock and fudge

Restart service

**Command:** 
```console
service ntpd restart
```
**Command:**
```console
ntpq -p -n
```
Now copy rpm for centos

**Command:** 
```console
rpm –import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5
```
**Command:** 
```console
yum -y install ntp
```
As the file is not copied so we will copy it again

**Command:** 
```console
scp node1:/etc/yum.repos.d/CentOS-Base.repo .
```
**Command:** 
```console
scp node1:/etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/
```
Now install again:

**Command:** 
```console
yum -y install ntp
```
**Setupping ntp service on node2.**

**Command:** 
```console
vi /etc/ntp.conf
```

Disable server 0, server 1, server 2

Disable server local-clock and fudge

Restart service

**Command:** 
```console
service ntpd restart
```

**Command:** 
```console
ntpq -p -n
```

Now copy rpm for centos

**Command:** 
```console
rpm –import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5
```
**Command:** 
```console
yum -y install ntp
```

As the file is not copied so we will copy it again

**Command:**
```console
scp node2:/etc/yum.repos.d/CentOS-Base.repo .
```
**Command:** 
```console
scp node2:/etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/
```
Now install again:

**Command:**
```console
yum -y install ntp
```
**Now configure the ntp file**

**Command:**
```console
vi /etc/ntp.conf
```
Add server 10.0.0.2 which is our host machine.

Disable server 0, sever1, server2

Restart service

**Command:** 
```console
service ntpd restart
```
Now check configuration

**Command:**
```console
chkconfig –level 35 ntpd on
```
**Command:** 
```console
ntpq -p -n
```
**Command:**
```console
watch &quot;ntpq -p -n&quot;
```
**Configure ntp on node1**

**Command:** 
```console
vi /etc/ntp.conf
```
Add server 10.0.0.2 which is our host machine.

Disable server 0, sever1, server2

Disable local server, fudge

Restart service

**Command:** 
```console
service ntpd restart
```
Now check configuration

**Command:** 
```console
chkconfig –level 35 ntpd on
```
**Command:**
```console
ntpq -p -n
```
**Command:** 
```console
watch &quot;ntpq -p -n&quot;
```
**Now copy these configurations on node2**

**Command:** 
```console
scp /etc/ntp.conf node2:/etc/ntp.conf
```
**Command:** 
```console
chkconfig –level 35 ntpd on
```
Restart service

**Command:** 
```console
service ntpd restart
```
Checking on the host machine if ntp is configured on all nodes.

**Command:** 
```console
watch &quot;ntpq -p -n&quot;
```
##


## **Installation of PDSH**

Check if pdsh is downloaded on the host machine or not.

**Command:**
```console
cd
```
**Command:** 
```console
ls
```
If it is not downloaded you can download it from the SourceForge website by typing pdsh on google search.

Now copy pdsh from masternode

**Command:** 
```console
scp 10.0.0.2:/root/pdsh\* .
```
Press yes

Enter the password which is red hat

It&#39;s copied.

Rebuild rpm

**Command:** 
```console
rpmbuild –rebuild pdsh-2.18-1.src.rpm
```
This is not mandatory for all nodes other than masternode

Changing directory

**Command:**
```console
 cd /usr/src/redhat/RPMS/i386/
```
**Command:** 
```console
rpm -ivh pdsh-\*
```
Now wait until it is debugging and installing

Now everything is installed and pdsh works.

What does pdsh do? If you want to perform a certain operation on all the nodes, or any specific nodes, one way is to manually log in through SSH to each node and perform the task and the second is you can just tell PD shell to do it at will go out and perform that task on all the nodes. It&#39;s very simple. So suppose you want to execute the date command on all the nodes or uptime command on all the nodes or whatever. So you would just tell PD shell to do it but in order for PD shell to work, it needs a machine file.

**Command:**
```console
vi /etc/machines
```
Add these three lines

masternode

node1

node2

These are the three nodes that I&#39;m going to use or which will be used for PD shall.

Now execute the pdsh on all nodes.

What executes what let&#39;s say date, is simple.

**Command:** 
```console
pdsh -a date
```
It went out on all the nodes and it brought the output back from all the notes you see it they&#39;re all 100% At the same time that&#39;s not the because of PDSH because of NTP which we just set up you Just go to masternode and enter.

**Command:**
```console
pdsh -a ntpq -p -n
```
## **Setup NFS**

Now setup nfs on masternode

Coming back to home directory

**Command:** 
```console
cd
```
**Command:** vi /etc/exports/

Add

/cluster \*(rw,no\_root\_squash,sync)

Save and exit

Restart NFS service

**Command:** service nfs restart

Check Configuration

**Command:** chkconfig –level 35 nfs on

Make a directory

**Command:** mkdir /cluster

Again restart service

**Command:** service nfs restart

Now we have to create this directory on all nodes so we will just use pdsh to create on all nodes at once

**Command:** pdsh -w node1,node2 mkdir /cluster

Now mounting

**Command:** df -hT

Execute this command on node1

**Command:** mount -t nfs masternode:/cluster /cluster/

Execute this command on node2

**Command:** mount -t nfs masternode:/cluster /cluster/

Now you can see that it is written that you have mounted it from the masternode.

**Now specify etc/fstab on node1**

**Command:** vi /etc/fstab

Add this line

masternode:/cluster /cluster nfs defaults 0 0

**Now specify etc/fstab on node2**

**Command:** vi /etc/fstab

Add this line

masternode:/cluster /cluster nfs defaults 0 0

## **Creation of ordinary user and also setup SSH equivalence**

**Group:** mpigroup-600

**User:** mpiuser-600

Member of mpigroup

The home directory will be /cluster/mpiuser

Now coming back to the masternode.

**Command:** groupadd -g 600 mpigroup

**Command:** useradd -u 600 -g 600 -d /cluster/mpiuser mpiuser

This directory is now created.

Now add group and users on node1 and node2

Run these commands on each node separately

**Command:** groupadd -g 600 mpigroup

**Command:** useradd -u 600 -g 600 -d /cluster/mpiuser mpiuser

Our users and groups are now created on all nodes.

Now we are doing user equivalence

**Command:** su - mpiuser

Generate its sshkeys as well

**Command:** ssh-keygen -t dsa

Press enter no need to enter paraphrase

**Command:** ssh-keygen -t rsa

Press enter no need to enter paraphrase

As two key pairs are generated

Now,

**Command:** ls /cluster

Switch to mpiuser

**Command:** su - mpiuser

**Command:** ls -l

Check all the files here

**Command:** ls -la

Now changing directory

**Command:** cd .ssh/

**Command:** ls -la

Remember /cluster directory is shared across all nodes.

Append the public keys into the authorized keys file

**Command:** cat \*.pub \&gt;\&gt; authorized\_keys

**Command:** cd ..

Now try to command as a mpiuser on all nodes

**Command:** ssh masternode uptime

**Command:** ssh node1 uptime

**Command:** ssh node2 uptime

Check hostname by ssh command

**Command:** ssh masternode hostname

**Command:** ssh node1 hostname

**Command:** ssh node2 hostname

Hostnames of each node must be visible by these commands.

Now check hostnames by PDSH

**Command:** pdsh -a hostname

## **Installation of prerequisites packages (GCC, G77, etc)**

Check if all nodes have GCC or not

**Command:** rpm -q GCC

The version of GCC will be visible

**Command:** rpm -qa | grep g77

If not shown by this command you can run

**Command:** yum list | grep g77

If g77 exists this will be visible there.

Install g77 on masternode

**Command:** yum -y install compat-gcc-34-g77

Installing g77 on node1 and node2 from masternode

**Command:** pdsh -w node1,node2 yum -y install compat-gcc-34-g77

All prerequisites are now installed.

## **Installation of MPI**

Now, we go for MPI installation.

So, MPI is basically Message Passing Interface is the language that is used to run a program specially designed program on multiple compute nodes on multiple nodes. MPI can be downloaded from various places there is open MPI this there are other MPI as well. I&#39;m going to download it from the web.

**Command:** scp root@10.0.0.2:/root/mpi\* .

Press yes

Enter password redhat

Mpi is downloaded in the home directory

**Command:** ls -lh

The file is not owned by mpiuser

**Command:** chown mpiuser:mpigroup /cluster -R

Access is now given to mpiuser

Switch user to mpiuser

**Command:** su - mpiuser

Moving mpi

**Command:** mv mpich2-1.0.8.tar.gz ..

**Command:** ls

**Command:** cd ..

**Command:** ls -lh

As you can see it is nowhere.

Now uncompressing

**Command:** tar xzf mpich2-1.0.8.tar.gz

**Command:** ls

**Command:** cd mpich2-1.0.8

**Command:** ls

There are so many files we are now configuring.

This will be a new directory.

**Command:**./Pictures/configure –prefix=/cluster/mpich2

All the parts which were left during the installation will be installed by this command.

**Command:** make

Now the files will move to /cluster directory

**Command:** make install

next, I&#39;m going to set up some environment variables in the MPI user&#39;s bash\_profile.

First goto home directory

**Command:** cd

**Command:** vi .bash\_profile

Add these lines there

PATH =$PATH:$HOME/bin:/cluster/mpich2/bin

LD\_LIBRARY\_PATH=$LD\_LIBRARY\_PATH:/cluster/mpich2/lib

export PATH

export LD\_LIBRARY\_PATH

If you don&#39;t want to logout

**Command:** source .bash\_profile

This will load the new values

You can also verify by the echo command

**Command:** echo $PATH

Check if it is able to find MPD

**Command:** which mpd

Check if it is able to find mpiexec

Command: which mpiexec

Check if it is able to find mpirun

**Command:** which mpirun

Create an mpd.host file

**Command:** cat \&gt;\&gt; /cluster/mpiuser/mpd.hosts \&lt;\&lt; EOF

**\&gt;** masternode

**\&gt;** node1

**\&gt;** node2

**\&gt;** EOF

Check the names here of all nodes

**Command:** cat \&gt;\&gt; /cluster/mpiuser/mpd.hosts

If you don&#39;t want your masternode to take part in any kind of computation follow the command below.

**Command:** vi /cluster/mpiuser/mpd.hostfile

Remove masternode from here and exit

Now creating secret files

**Command:** vi /cluster/mpiuser/.mpd.conf

Add this line

secretword=redhat

Save and exit

Boot mpt on compute nodes

**Command:** mpd &amp;

If it has permission issue follow below command

**Command:** chmod 0600 /cluster/mpiuser/.mpd.conf

**Command:** ps aux | grep mpd

Now again Booting mpt on compute nodes

**Command:** mpd &amp;

Checking if it&#39;s running

**Command:** mpdtrace -l

Exit all

**Command:** mpdallexit

**Command:** mpdboot -n 2 --chkuponly

Now you can see 2 hosts are up

**Command:** ps aux | grep mpd

Now edit this file

**Command:** vi /cluster/mpiuser/mpd.hosts

Add this line

Masternode

Save and exit

Checking how many servers are up

**Command:** mpdboot -n 3 --chkuponly

Now you can see 3 hosts are up

**Command:** mpdboot -n 3

**Command:** mpdtrace

Now exit from all

**Command:** mpdexitall

Now check if I am traced or not

**Command:** mpdtrace

Run each command separately and see the time difference

**Command:** mpiexec -n 1 ./Pictures/cpi

As you can see execution time

**Command:** mpiexec -n 2 ./Pictures/cpi

**Command:** mpiexec -n 3 ./Pictures/cpi

Compiling a program

**Command:** mpicc -o icpi icpic.c

**Command:** ls

It&#39;s compiled.

**Command:** mpiexec -n 1 ./Pictures/icpi

Enter any large random number and see the execution time.

Now run this using 2 nodes

**Command:** mpiexec -n 1 ./Pictures/icpi

Enter the same number and see the execution time difference.

On virtual machines, it might give higher time but in physical servers, it will be okay sometimes it gets problematic in VM&#39;s.
![Screenshot](./Pictures/differencebetweenoneandthreenodesprocessing.PNG)

Remember real hardware clusters will give much accuracy and proficiency.

## **Compiling Linpack**

For linpack, you would need a BLAS library.

Check if it already exists or not

**Command:** cd

**Command:** ls

**Command:** scp 10.0.0.2:/root/G\* .

Enter root password

Copy file

**Command:** cp /cluster/mpiuser/

**Command:** cp GotoBLAS-1.26.tar.gz /cluster/mpiuser/

Switching user

**Command:** su - mpiuser

**Command:** ls

Uncompressing

**Command:** tar xzf GotoBLAS-1.26.tar.gz

It will create a directory here

**Command:** ls -l

As it is seen, a directory is created.

BLAS is a linear algebra library

**Command:** ls

**Command:** vi Makefile.rule

It has this online 16. As you can see here, this Fortran compiler is g 77. Some of the documentation or guides will tell you to uncomment this. But I&#39;ll tell you not to because I&#39;m exiting without let&#39;s undo, exit without changes. The reason is simple: official documentation tells us that it will use G 77 If it does not find Fortran 77. So, if g 77 is going to be used anywhere, don&#39;t waste time going into this file and editing it. What you want to do now is you are going to compile it.

**Command:**./Pictures/quickbuild.

**Command:**./Pictures/quickbuild.32bit

**Command:** make

It is compiled now.

Now you would need to download a high-performance linpack.

You can download it from [www.netlib.org/benchmark/hpl](http://www.netlib.org/benchmark/hpl)

I am copying it from my host machine

**Command:** scp root@10.0.0.2:/root/hpl\* .

Enter password redhat

Check now if the file is here

**Command:** ls

The file is in the home directory of this mpiuser.

Extract or uncompress

**Command:** tar xzf hpl.tgz

**Command:** ls

**Command:** cd hpl.tgz

**Command:** cd hpl

**Command:** ls

Copying setup

**Command:** cp setup/

**Command:** cp setup/Make.Linux\_pII\_FBLAS\_gm .

Copying to the current location

Check your GCC version

**Command:** gcc -v

**Command:** ls /usr/lib/

Press yes

**Command:** ls /usr/lib/gcc

**Command:** ls /usr/lib/gcc/i386-redhat-linux/

Select version

**Command:** ls /usr/lib/gcc/i386-redhat-linux/4.1.2/

Check current location

**Command:** pwd

**Command:** vi Make.Linux\_PII\_FBLAS\_gm

Change LA Directory in this file to

**$** (HOME) / GotoBLAS

Change LA Library

**$** (LAdir) / libgoto.a -lm -L/usr/lib/gcc/i386/-redhat-linux/4.1.2

Change CC Flags

**$** (HPL\_DEFS) -03

Change Linker

**$** mpicc

Save and exit

## **Benchmarking**

Now build this

**Command:** make arch=Linux\_PII\_FBLAS\_gm

Moving to this directory

**Command:** ls /cluster/mpiuser/hpl/bin/Linux\_PII\_FBLAS\_gm/

List here

**Command:** ls

Copy HPL.dat

**Command:** cp HPL.dat HPL.dat.orig

**Command:** vi HPL.dat

Now the linpack configuration file has appeared.

value from size can be found first, by

**Command:** free -b

Go to calculator

**Command:** bc

Sqrt (.1\*(value of the output of your free b) \* 2)

5997.8 approx 6000

Now edit this file

**Command:** vi HPL.dat

Edit No of problem to 1

Size 6000

No of block 1

Size of block 100

Process grid 1

The processor on each node 1

Processor quantity 2

Save and exit

First exit

**Command:** mpdallexit

Boot again:

**Command:** mpdboot -n 2

It is not reading mpd.host file

Goto cd

**Command:** cd

Boot again:

**Command:** mpdboot -n 2

It&#39;s booted.

Going to the previous directory

**Command:** cd -

Check current directory

**Command:** pwd

Now execute hpl program

**Command:** mpiexec -n 2 ./Pictures/xhpl

This is our benchmarking being done. This might take some time.

You can see complete passing and failing reports at the end of the benchmarking process.

Now execute hpl programe and send output to textfile

**Command:** mpiexec -n 2 ./Pictures/xhpl \&gt; performance.txt