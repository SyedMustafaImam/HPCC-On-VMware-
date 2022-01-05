
---

<p style='color:#FAF9F6;font-size:32px; font-weight:bold'> Parallel &amp; Distributed Computing </p>

<!-- PROJECT LOGO -->
<br />
<div align="center">

[![x][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]

<br />
<br />
<br />

  <a href="https://github.com/SyedMustafaImam/HPCC-On-VMware-">
    <img src="Pictures/logo.png" alt="Logo" >
  </a>

<div id="top"></div>

<p style='font-size:32px; font-weight:bold'>Parallel &amp; Distributed Computing </p>
  <h3 align="center">HPC Cluster Configuration</h3>

  <p align="center">
    This documentation will help you create a hpcc system on vmware.
    <br />
    <a href="https://github.com/SyedMustafaImam/HPCC-On-VMware-"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/SyedMustafaImam/HPCC-On-VMware-">Tutorial</a>
    ·
    <a href="https://github.com/SyedMustafaImam/HPCC-On-VMware-/issues">Softwares</a>
    ·
    <a href="https://github.com/SyedMustafaImam/HPCC-On-VMware-/issues">Issues</a>
  </p>

<p style='font-size:21.4px; font-weight:bold'>Project Report</p>
<p style='font-size:15.1px; font-weight:bold'>Section: BSCS 7A</p>

<p style='font-size:15.1px; font-weight:bold'>By</p>
<p style='font-size:15.1px;'>

[Syed Mustafa Imam][linkedin-url-mustafa]

[Syed Hurrar Hassan Rizvi][linkedin-url-hurrar]

[Elliott Franscis Joseph][linkedin-url-elliott]

[Hirdesh Kumar][linkedin-url-hirdesh]

</div>

<br />

---

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
- [**3.Steps**](#3steps)
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

<p align="right">(<a href="#top">back to top</a>)</p>

# **2.Use Cases**

An HPC is Deployed on-premises, at the edge, or in the cloud. HPC solutions are used for a variety of purposes across multiple industries.HPC is used to help scientists find sources of renewable energy, understand the evolution of our universe. Predict and track the storms, and create new materials.

<p align="right">(<a href="#top">back to top</a>)</p>

## **Research Labs**

HPC is used to help scientists find sources of renewable energy, understand the evolution of our universe, predict and track storms and create new materials.

<p align="right">(<a href="#top">back to top</a>)</p>

## **Media And Entertainment**

HPC is used to edit feature films, render mind-blowing special effects, and stream live events around the world.

<p align="right">(<a href="#top">back to top</a>)</p>

## **Oil and gas**

HPC is used to more accurately identify where to drill for new wells and to help boost production from existing wells.

<p align="right">(<a href="#top">back to top</a>)</p>

## **Artificial Intelligence**

HPC is used to detect credit card fraud, provide self-guided technical support, reach self-driving vehicles, and improve cancer screening techniques.

<p align="right">(<a href="#top">back to top</a>)</p>

## **Financial Services**

HPC is used to track real-time stock trends and automate trading.

<p align="right">(<a href="#top">back to top</a>)</p>

# **3.Steps**

## **Creation Of Virtual Machines**

The master node is set up by the name &#39;HPC Master&#39; with Red Hat Enterprise Linux 32 bit as the main OS of the Virtual Machine and the network working on a bridge network. The System Configuration of the HPC Master is presented below:

![ScreenShot](./Pictures/master.JPG)

The compute node is also created by the name &#39;node1&#39; with Red Hat Enterprise Linux 32 bit as the main OS of the Virtual Machine with a standard data store and a bridged network. The System Configuration of the HPCNode1 are presented below:

![ScreenShot](./Pictures/node1.JPG)

Another compute node is also created by the name &#39;node2&#39; with Red Hat Enterprise Linux 32 bit as the main OS of the Virtual Machine with a standard data store and a bridged network. The System Configuration of the HPCNode2 are presented below:

![ScreenShot](./Pictures/node2.JPG)

An NTP server was also created by using a node that is not part computation performed by a cluster. It was done by using Ubuntu OS 64 bit as the main OS of the Virtual Machine with a standard data store and a NAT network. System Configurations are presented below:

![ScreenShot](./Pictures/ntp.JPG)

<p align="right">(<a href="#top">back to top</a>)</p>

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

**Command:**

```console
[root@hostmachine ~]# cd machines
```

**Command:**

```console
[root@hostmachine machines]# ls
```

And we have this HPC master directory, which we have these files.

Let&#39;s enter into this directory by

**Command:**

```console
[root@hostmachine machines]# cd HPCMaster
```

**Command:**

```console
[root@hostmachine HPCMaster]# ls
```

**Command:**

```console
[root@hostmachine HPCMaster]# ls -lh
```

As you can see, this is your virtual machine disk file named **HPCMaster.vmdk** , which consumes 1.6 GB.

So now I&#39;m copying this file.

**Command:**

```console
[root@hostmachine HPCMaster]# ls -lh ../HPCNode1/
```

As you can see you have four files there. Now we will copy this VMDK file from here and overwrite this VMDK file here.

**Command:**

```console
[root@hostmachine HPCMaster]# cp HPCMaster.vmdk ../Pictures/HPCNode1/HPCNode1.vmdk
```

Press y for yes overwriting.

As you can see the file is copied so let&#39;s check the list.

**Command:**

```console
[root@hostmachine HPCMaster]# ls ../HPCNode1/ -lh
```

Let&#39;s try starting node1 and see what happens. Click power on and go to the console window and let it boot up. It will have all settings from your HPC master. That means it will also have the same hostname, same IP everything.

Once this is booted up. So let&#39;s go to the console, it will seem like a master node, but it is not it is, as you can see here, this is **HPCNode1** and in the same way, we&#39;ll do the second node as well. But first, adjust the hostnames.

**Command:**

```console
[root@masternode ~]# vi /etc/sysconfig/network
```

Then edit hostname as **Node1**

And the IP is going to be

**Command:**

```console
[root@masternode ~]# vi /etc/sysconfig/network-scripts/ifcfg-eth0
```

Life config Ethernet zero should not get its IP from DHCP. It&#39;s going to be a static IP address equal to 10.0.0.11 and netmask is equal to 255.255.255.0

One more thing to see hosts.

**Command:**

```console
[root@masternode ~]# vi /etc/hosts
```

remove this master node at all from the script.

Now let&#39;s change the hostname manually.

**Command:**

```console
[root@masternode ~]# hostname node1
```

**Command:**

```console
[root@masternode ~]# service syslog restart
```

**Command:**

```console
[root@masternode ~]# less /var/log/messages
```

That will make sure that the logs in the various log messages are written correctly.

Press **shift G** you can see as soon as you&#39;ve restarted Syslog the logs here it says node1 now before it was master node.

Then reboot this system

**Command:**

```console
[root@masternode ~]# reboot
```

Now repeat the same process for Node2 as you have done for the Node1.

<p align="right">(<a href="#top">back to top</a>)</p>

## **Configuring etc host file**

**Command:**

```console
[root@masternode ~]# vi /etc/hosts
```

Now delete IP version 6 naming file

Then remove a master node from this localhost line

Add three lines here

10.0.0.20 master node

10.0.0.11 node1

10.0.0.12 node2

Then back to the console.

**Command:**

```console
[root@masternode ~]# scp /etc/hosts node1:/etc/ 
```

Except for the fingerprint of node1, node1&#39;s password is redhat.

Do the same thing for node2

**Command:**

```console
[root@masternode ~]# scp /etc/hosts node2:/etc/
```

Except for the fingerprint of node2, node2&#39;s password is redhat.

Now, the, etc hosts file is configured.

<p align="right">(<a href="#top">back to top</a>)</p>

## **SSH equivalence establishment for user root**

Now we will generate public and private keys (DSA and RSA) of all nodes.

Generate dsa keys

**Command:**

```console
[root@masternode ~]# ssh-keygen -t dsa
```

Just press enter, no need to enter a passphrase.

Now generate the rsa keys

**Command:**

```console
[root@masternode ~]# ssh-keygen -t rsa
```

Just press enter, no need to enter a passphrase.

Now if you want you can check these keys

**Command:**

```console
[root@masternode ~]# cd .ssh/
```

**Command:**

```console
[root@masternode .ssh]# ls -l
```

As you can see both dsa and rsa are visible along with the public and private keys.

Now copy all four key files for this directory

**Command:**

```console
[root@masternode .ssh]# cd ..
```

**Command:**

```console
[root@masternode ~]# scp -r .ssh node1:/root/
```

Enter the password which is redhat

As files are copied in node 1 now do the same process for node 2.

**Command:**

```console
[root@masternode ~]# scp -r .ssh node2:/root/
```

Now do one more step

**Command:**

```console
[root@masternode ~]# cd .ssh/
```

**Command:**

```console
[root@masternode .ssh]# cat *.pub >> authorized\_keys
```

**Command:**

```console
[root@masternode .ssh]# cd ..
```

Now copy these files on both nodes again

**Command:**

```console
[root@masternode ~]# scp -r .ssh node1:/root/
```

Enter the password which is redhat

As files are copied in node 1 now do the same process for node 2.

**Command:**

```console
[root@masternode ~]# scp -r .ssh node2:/root/
```

Now We will generate RSA fingerprints,

**Command:**

```console
[root@masternode ~]# ssh-keyscan -t dsa masternode node1 node2
```

Now I&#39;m going to put it in a special file on this log

**Command:**

```console
[root@masternode ~]# ssh-keyscan -t dsa masternode node1 node2 > /etc/ssh/ssh_known_hosts
```

You see this file. This file is a valid one, but it does not exist by default. Now what I&#39;m going to do is I&#39;m going to scan the RSA keys of the same nodes and I&#39;m going to append that to this file.

**Command:**

```console
[root@masternode ~]# ssh-keyscan -t rsa masternode node1 node2 >> /etc/ssh/ssh_known_hosts
```

Now see how the file looks like

**Command:**

```console
[root@masternode ~]# less /etc/ssh/ssh_known_hosts
```

Now replicate this file to all nodes.

**Command:**

```console
[root@masternode ~]# scp /etc/ssh/ssh_known_hosts node1:/etc/ssh
```

**Command:**

```console
[root@masternode ~]# scp /etc/ssh/ssh_known_hosts node2:/etc/ssh
``` 

**Testing by logging it into each node**

**Command:**

```console
[root@masternode ~]# ssh masternode
```

**Command:**

```console
[root@masternode ~]# exit
```

**Command:**

```console
[root@node1 ~]# ssh node1
```

**Command:**

```console
[root@node1 ~]# exit
```

**Command:**

```console
[root@masternode ~]# ssh node2
```

**Command:**

```console
[root@node2 ~]# exit  
```

**Testing by logging all nodes into each other node**

**Command:**

```console
[root@node1 ~]# ssh masternode uptime
```


**Command:**

```console
[root@node1 ~]# ssh node1 uptime
```

**Command:**

```console
[root@node1 ~]# ssh node2 uptime
```


<p align="right">(<a href="#top">back to top</a>)</p>

## **Setup NTP Service**

**Setupping NTP service on node1.**

**Command:**

```console
[root@node1 ~]# vi /etc/ntp.conf
```

Disable server 0, server 1, server 2

Disable server local-clock and fudge

Restart service

**Command:**

```console
[root@node1 ~]# service ntpd restart
```

**Command:**

```console
[root@node1 ~]# ntpq -p -n
```

Now copy rpm for centos

**Command:**

```console
[root@node1 ~]# rpm –-import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5
```

**Command:**

```console
[root@node1 ~]# yum -y install ntp
```

As the file is not copied so we will copy it again

**Command:**

```console
[root@node1 ~]# scp node1:/etc/yum.repos.d/CentOS-Base.repo .
```

**Command:**

```console
[root@node1 ~]# scp node1:/etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/
```

Now install again:

**Command:**

```console
[root@masternode ~]# yum -y install ntp
```

**Setupping ntp service on node2.**

**Command:**

```console
[root@node2 ~]# vi /etc/ntp.conf
```

Disable server 0, server 1, server 2

Disable server local-clock and fudge

Restart service

**Command:**

```console
[root@node2 ~]# service ntpd restart
```

**Command:**

```console
[root@node2 ~]# ntpq -p -n
```

Now copy rpm for centos

**Command:**

```console
[root@node2 ~]# rpm –import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5
```

**Command:**

```console
[root@node2 ~]# yum -y install ntp
```

As the file is not copied so we will copy it again

**Command:**

```console
[root@node2 ~]# scp node2:/etc/yum.repos.d/CentOS-Base.repo .
```

**Command:**

```console
[root@node2 ~]# scp node2:/etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/
```

Now install again:

**Command:**

```console
[root@node2 ~]# yum -y install ntp
```

**Now configure the ntp file**

**Command:**

```console
[root@masternode ~]# vi /etc/ntp.conf
```

Add server 10.0.0.2 which is our host machine.

Disable server 0, sever1, server2

Restart service

**Command:**

```console
[root@masternode ~]# service ntpd restart
```

Now check configuration

**Command:**

```console
[root@masternode ~]# chkconfig -–level 35 ntpd on
```

**Command:**

```console
[root@masternode ~]# ntpq -p -n
```

**Command:**

```console
[root@masternode ~]# watch "ntpq -p -n"
```

**Configure ntp on node1**

**Command:**

```console
[root@node1 yum.repos.d]# vi /etc/ntp.conf
```

Add server 10.0.0.2 which is our host machine.

Disable server 0, sever1, server2

Disable local server, fudge

Now check configuration

```console
[root@node1 yum.repos.d]# chkconfig -–level 35 ntpd on
```
Restart service
**Command:**

```console
[root@node1 yum.repos.d]# service ntpd restart
```

Checking on the host machine if ntp is configured on all nodes.
**Command:**

```console
[root@node1 yum.repos.d]# ntpq -p -n
```

**Command:**

```console
[root@node1 yum.repos.d]# watch "ntpq -p -n";
```

**Now copy these configurations on node2**

**Command:**

```console
[root@node1 yum.repos.d]# scp /etc/ntp.conf node2:/etc/ntp.conf
```

**Command:**

```console
[root@node2 ~]# chkconfig –level 35 ntpd on
```

Restart service

**Command:**

```console
[root@node2 ~]# service ntpd restart
```

Checking on the host machine if ntp is configured on all nodes.

**Command:**

```console
[root@node1 yum.repos.d]# watch "ntpq -p -n"
```

##

<p align="right">(<a href="#top">back to top</a>)</p>

## **Installation of PDSH**

Check if pdsh is downloaded on the host machine or not.

**Command:**

```console
[root@hostmachine centos]# cd
```

**Command:**

```console
[root@hostmachine ~]# ls
```

If it is not downloaded you can download it from the SourceForge website by typing pdsh on google search.

Now copy pdsh from masternode

**Command:**

```console
[root@masternode ~]# scp 10.0.0.2:/root/pdsh* .
```

Type yes

Enter the password which is red hat

It&#39;s copied.

Rebuild rpm

**Command:**

```console
[root@masternode ~]# rpmbuild –rebuild pdsh-2.18-1.src.rpm
```

This is not mandatory for all nodes other than masternode

Changing directory

**Command:**

```console
[root@masternode ~]# cd /usr/src/redhat/RPMS/i386/
```

**Command:**

```console
[root@masternode i386]# rpm -ivh pdsh-*
```

Now wait until it is debugging and installing

Now everything is installed and pdsh works.

What does pdsh do? If you want to perform a certain operation on all the nodes, or any specific nodes, one way is to manually log in through SSH to each node and perform the task and the second is you can just tell PD shell to do it at will go out and perform that task on all the nodes. It&#39;s very simple. So suppose you want to execute the date command on all the nodes or uptime command on all the nodes or whatever. So you would just tell PD shell to do it but in order for PD shell to work, it needs a machine file.

**Command:**

```console
[root@masternode i386]# vi /etc/machines
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
[root@masternode i386]# pdsh -a date
```

It went out on all the nodes and it brought the output back from all the notes you see it they&#39;re all 100% At the same time that&#39;s not the because of PDSH because of NTP which we just set up you Just go to masternode and enter.

**Command:**

```console
[root@masternode i386]# pdsh -a ntpq -p -n
```

<p align="right">(<a href="#top">back to top</a>)</p>

## **Setup NFS**

Now setup nfs on masternode

Coming back to home directory

**Command:**

```console
cd
```

**Command:**

```console
vi /etc/exports/
```

Add

```console
/cluster \*(rw,no\_root\_squash,sync)
```

Save and exit

Restart NFS service

**Command:**

```console
service nfs restart
```

Check Configuration

**Command:**

```console
chkconfig –level 35 nfs on
```

Make a directory

**Command:**

```console
mkdir /cluster
```

Again restart service

**Command:**

```console
service nfs restart
```

Now we have to create this directory on all nodes so we will just use pdsh to create on all nodes at once

**Command:**

```console
pdsh -w node1,node2 mkdir /cluster
```

Now mounting

**Command:**

```console
df -hT
```

Execute this command on node1

**Command:**

```console
mount -t nfs masternode:/cluster /cluster/
```

Execute this command on node2

**Command:**

```console
mount -t nfs masternode:/cluster /cluster/
```

Now you can see that it is written that you have mounted it from the masternode.

**Now specify etc/fstab on node1**

**Command:**

```console
vi /etc/fstab
```

Add this line

masternode:/cluster /cluster nfs defaults 0 0

**Now specify etc/fstab on node2**

**Command:**

```console
vi /etc/fstab
```

Add this line

masternode:/cluster /cluster nfs defaults 0 0

<p align="right">(<a href="#top">back to top</a>)</p>

## **Creation of ordinary user and also setup SSH equivalence**

**Group:** mpigroup-600

**User:** mpiuser-600

Member of mpigroup

The home directory will be /cluster/mpiuser

Now coming back to the masternode.

**Command:**

```console
 groupadd -g 600 mpigroup
```

**Command:**

```console
useradd -u 600 -g 600 -d /cluster/mpiuser mpiuser
```

This directory is now created.

Now add group and users on node1 and node2

Run these commands on each node separately

**Command:**

```console
groupadd -g 600 mpigroup
```

**Command:**

```console
useradd -u 600 -g 600 -d /cluster/mpiuser mpiuser
```

Our users and groups are now created on all nodes.

Now we are doing user equivalence

**Command:**

```console
su - mpiuser
```

Generate its sshkeys as well

**Command:**

```console
ssh-keygen -t dsa
```

Press enter no need to enter paraphrase

**Command:**

```console
ssh-keygen -t rsa
```

Press enter no need to enter paraphrase

As two key pairs are generated

Now,

**Command:**

```console
ls /cluster
```

Switch to mpiuser

**Command:**

```console
su - mpiuser
```

**Command:**

```console
ls -l
```

Check all the files here

**Command:**

```console
ls -la
```

Now changing directory

**Command:**

```console
cd .ssh/
```

**Command:**

```console
ls -la
```

Remember /cluster directory is shared across all nodes.

Append the public keys into the authorized keys file

**Command:**

```console
cat \*.pub \&gt;\&gt; authorized\_keys
```

**Command:**

```console
cd ..
```

Now try to command as a mpiuser on all nodes

**Command:**

```console
ssh masternode uptime
```

**Command:**

```console
ssh node1 uptime
```

**Command:**

```console
ssh node2 uptime
```

Check hostname by ssh command

**Command:**

```console
ssh masternode hostname
```

**Command:**

```console
ssh node1 hostname
```

**Command:**

```console
ssh node2 hostname
```

Hostnames of each node must be visible by these commands.

Now check hostnames by PDSH

**Command:**

```console
pdsh -a hostname
```

<p align="right">(<a href="#top">back to top</a>)</p>

## **Installation of prerequisites packages (GCC, G77, etc)**

Check if all nodes have GCC or not

**Command:**

```console
rpm -q GCC
```

The version of GCC will be visible

**Command:**

```console
rpm -qa | grep g77
```

If not shown by this command you can run

**Command:**

```console
yum list | grep g77
```

If g77 exists this will be visible there.

Install g77 on masternode

**Command:**

```console
yum -y install compat-gcc-34-g77
```

Installing g77 on node1 and node2 from masternode

**Command:**

```console
pdsh -w node1,node2 yum -y install compat-gcc-34-g77
```

All prerequisites are now installed.

<p align="right">(<a href="#top">back to top</a>)</p>

## **Installation of MPI**

Now, we go for MPI installation.

So, MPI is basically Message Passing Interface is the language that is used to run a program specially designed program on multiple compute nodes on multiple nodes. MPI can be downloaded from various places there is open MPI this there are other MPI as well. I&#39;m going to download it from the web.

**Command:**

```console
scp root@10.0.0.2:/root/mpi\* .
```

Press yes

Enter password redhat

Mpi is downloaded in the home directory

**Command:**

```console
ls -lh
```

The file is not owned by mpiuser

**Command:**

```console
chown mpiuser:mpigroup /cluster -R
```

Access is now given to mpiuser

Switch user to mpiuser

**Command:**

```console
su - mpiuser
```

Moving mpi

**Command:**

```console
mv mpich2-1.0.8.tar.gz ..
```

**Command:**

```console
ls
```

**Command:**

```console
cd ..
```

**Command:**

```console
ls -lh
```

As you can see it is nowhere.

Now uncompressing

**Command:**

```console
tar xzf mpich2-1.0.8.tar.gz
```

**Command:**

```console
ls
```

**Command:**

```console
cd mpich2-1.0.8
```

**Command:**

```console
ls
```

There are so many files we are now configuring.

This will be a new directory.

**Command:**

```console
./Pictures/configure –prefix=/cluster/mpich2
```

All the parts which were left during the installation will be installed by this command.

**Command:**

```console
make
```

Now the files will move to /cluster directory

**Command:**

```console
make install
```

next, I&#39;m going to set up some environment variables in the MPI user&#39;s bash\_profile.

First goto home directory

**Command:**

```console
cd
```

**Command:**

```console
vi .bash\_profile
```

Add these lines there

```console
$PATH:$HOME/bin:/cluster/mpich2/bin
```

LD\_LIBRARY\_PATH=$LD\_LIBRARY\_PATH:/cluster/mpich2/lib

export PATH

export LD\_LIBRARY\_PATH

If you don&#39;t want to logout

**Command:**

```console
source .bash\_profile
```

This will load the new values

You can also verify by the echo command

**Command:**

```console
echo $PATH
```

Check if it is able to find MPD

**Command:**

```console
which mpd
```

Check if it is able to find mpiexec

Command: which mpiexec

Check if it is able to find mpirun

**Command:**

```console
which mpirun
```

Create an mpd.host file

**Command:**

```console
cat \&gt;\&gt; /cluster/mpiuser/mpd.hosts \&lt;\&lt; EOF
```

**\&gt;** masternode

**\&gt;** node1

**\&gt;** node2

**\&gt;** EOF

Check the names here of all nodes

**Command:**

```console
cat \&gt;\&gt; /cluster/mpiuser/mpd.hosts
```

If you don&#39;t want your masternode to take part in any kind of computation follow the command below.

**Command:**

```console
vi /cluster/mpiuser/mpd.hostfile
```

Remove masternode from here and exit

Now creating secret files

**Command:**

```console
vi /cluster/mpiuser/.mpd.conf
```

Add this line

secretword=redhat

Save and exit

Boot mpt on compute nodes

**Command:**

```console
mpd &amp;
```

If it has permission issue follow below command

**Command:**

```console
chmod 0600 /cluster/mpiuser/.mpd.conf
```

**Command:**

```console
ps aux | grep mpd
```

Now again Booting mpt on compute nodes

**Command:**

```console
mpd &amp;
```

Checking if it&#39;s running

**Command:**

```console
mpdtrace -l
```

Exit all

**Command:**

```console
mpdallexit
```

**Command:**

```console
mpdboot -n 2 --chkuponly
```

Now you can see 2 hosts are up

**Command:**

```console
ps aux | grep mpd
```

Now edit this file

**Command:**

```console
vi /cluster/mpiuser/mpd.hosts
```

Add this line

Masternode

Save and exit

Checking how many servers are up

**Command:**

```console
mpdboot -n 3 --chkuponly
```

Now you can see 3 hosts are up

**Command:**

```console
mpdboot -n 3
```

**Command:**

```console
mpdtrace
```

Now exit from all

**Command:**

```console
mpdexitall
```

Now check if I am traced or not

**Command:**

```console
mpdtrace
```

Run each command separately and see the time difference

**Command:**

```console
mpiexec -n 1 ./Pictures/cpi
```

As you can see execution time

**Command:**

```console
mpiexec -n 2 ./Pictures/cpi
```

**Command:**

```console
mpiexec -n 3 ./Pictures/cpi
```

Compiling a program

**Command:**

```console
mpicc -o icpi icpic.c
```

**Command:**

```console
ls
```

It&#39;s compiled.

**Command:**

```console
mpiexec -n 1 ./Pictures/icpi
```

Enter any large random number and see the execution time.

Now run this using 2 nodes

**Command:**

```console
mpiexec -n 1 ./Pictures/icpi
```

Enter the same number and see the execution time difference.

On virtual machines, it might give higher time but in physical servers, it will be okay sometimes it gets problematic in VM&#39;s.
![Screenshot](./Pictures/differencebetweenoneandthreenodesprocessing.PNG)

Remember real hardware clusters will give much accuracy and proficiency.

<p align="right">(<a href="#top">back to top</a>)</p>

## **Compiling Linpack**

For linpack, you would need a BLAS library.

Downlad the gotoblas library from here: https://www.tacc.utexas.edu/documents/1084364/1087496/GotoBLAS2-1.13.tar.gz/b58aeb8c-9d8d-4ec2-b5f1-5a5843b4d47b

You can download in the host machine and then copy it to master node.

**Command:**

```console
[root@hostmachine ~]# scp  -r GotoBLAS2-1.13.tar.gz root@10.0.0.20:/masternode/
```

Enter root's password

Now go to the master node and check it. 

**Command:**

```console
[root@masternode ~]# ls
```

Copy file

**Command:**

```console
[root@masternode ~]# cp GotoBLAS2-1.13.tar.gz /cluster/mpiuser/
```

Switching user

**Command:**

```console
[root@masternode ~]#  su - mpiuser
```

**Command:**

```console
[mpiuser@masternode ~]# ls -al
```

Uncompressing

**Command:**

```console
[mpiuser@masternode ~]# tar xzf GotoBLAS2-1.13.tar.gz
```

It will create a directory here

**Command:**

```console
[mpiuser@masternode ~]# cd GotoBLAS3-1.13
```

As it is seen, a directory is created.

BLAS is a linear algebra library

**Command:**

```console
[mpiuser@masternode GotoBLAS3-1.13]# ls
```

**Command:**

```console
[mpiuser@masternode GotoBLAS3-1.13]# make BIN=32
```

**Command:**

```console
[mpiuser@masternode GotoBLAS3-1.13]#  gmake TARGET=NEHALEM
```

It is compiled now.

Now you would need to download a high-performance linpack.

You can download it from [www.netlib.org/benchmark/hpl](https://www.netlib.org/benchmark/hpl/hpl-2.3.tar.gz)

Now copy it from the host machine

**Command:**

```console
[root@hostmachine ~]# scp -r hpl-2.3.tar.gz mpiuser@10.0.0.20:/cluster/mpiuser/
```

Enter password:

Check now if the file is here

**Command:**

```console
[mpiuser@masternode ~]# ls
```

The file is in the home directory of this mpiuser.

Extract or uncompress

**Command:**

```console
[mpiuser@masternode ~]# tar xzf hpl.tgz
```

**Command:**

```console
[mpiuser@masternode ~]# ls
```

**Command:**

```console
[mpiuser@masternode ~]# cd hpl
```

**Command:**

```console
[mpiuser@masternode ~]# ls
```

Copying setup

**Command:**

```console
[mpiuser@masternode hpl]# cp setup/Make.Linux_pII_FBLAS_gm .
```

Copying to the current location

Check your GCC version

**Command:**

```console
[mpiuser@masternode hpl]#  gcc -v
```

Select version

**Command:**

```console
[mpiuser@masternode hpl]# cd /usr/lib/gcc/i386-redhat-linux/4.1.2/
```

Check current location

**Command:**

```console
[mpiuser@masternode 4.1.2]#  pwd
```

**Command:**

```console
[mpiuser@masternode hpl]# vi Make.Linux_PII_FBLAS_gm
```

Change LA Directory in this file to

**$** (HOME) / GotoBLAS

Change LA Library

**$** (LAdir)/libgoto.a -lm -L/usr/lib/gcc/i386-redhad-linux/4.1.2

Change CC Flags

**$** (HPL\_DEFS) -03

Change Linker

**$** mpicc

Save and exit

<p align="right">(<a href="#top">back to top</a>)</p>

## **Benchmarking**

Now build this

**Command:**

```console
[mpiuser@masternode hpl]#  make arch=Linux_PII_FBLAS_gm
```

Moving to this directory

**Command:**

```console
[mpiuser@masternode hpl]# cd /cluster/mpiuser/hpl/bin/Linux_PII_FBLAS_gm/
```

List here

**Command:**

```console
[mpiuser@masternode Linux_PII_FBLAS_gm]# ls
```

Copy HPL.dat

**Command:**

```console
[mpiuser@masternode Linux_PII_FBLAS_gm]# cp HPL.dat HPL.dat.orig
```

**Command:**

```console
[mpiuser@masternode Linux_PII_FBLAS_gm]# vi HPL.dat
```

Now the linpack configuration file has appeared.

value from size can be found first, nothing to change.

**Command:**

```console
[mpiuser@masternode Linux_PII_FBLAS_gm]# free -b
```

Go to calculator on node2

**Command:**

```console
[root@node2 ~]# bc

< Sqrt (.1\*(value of the output of your free b) \* 2)

> 5997.8 approx 6000
```

Now edit this file on master node

**Command:**

```console
[mpiuser@masternode Linux_PII_FBLAS_gm]# vi HPL.dat
```

Edit No of problem to 1

Size 6000

No of block 1

Size of block 100

Process grid 1

The processor on each node 1

Processor quantity 2

Save and exit

First exit

**Command:**

```console
[mpiuser@masternode Linux_PII_FBLAS_gm]# mpdallexit
```

Boot again:

**Command:**

```console
[mpiuser@masternode Linux_PII_FBLAS_gm]# mpdboot -n 2
```

Now execute hpl program

**Command:**

```console
[mpiuser@masternode Linux_PII_FBLAS_gm]# mpiexec -n 2 ./xhpl
```

![ScreenShot](Pictures/benchmarkingStarted.png)

This is our benchmarking being started. This might take some time.

You can see complete passing and failing reports at the end of the benchmarking process.

![ScreenShot](Pictures/benchmarkingDone.png)

Now execute hpl programe and send output to textfile

**Command:**

```console
[mpiuser@masternode Linux_PII_FBLAS_gm]# mpiexec -n 2 ./xhpl > performance.txt
```

[contributors-shield]: https://img.shields.io/github/contributors/othneildrew/Best-README-Template.svg?style=for-the-badge
[contributors-url]: https://github.com/SyedMustafaImam/HPCC-On-VMware-/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/othneildrew/Best-README-Template.svg?style=for-the-badge
[forks-url]: https://github.com/SyedMustafaImam/HPCC-On-VMware-/network/members
[stars-shield]: https://img.shields.io/github/stars/othneildrew/Best-README-Template.svg?style=for-the-badge
[stars-url]: https://github.com/SyedMustafaImam/HPCC-On-VMware-/stargazers
[issues-shield]: https://img.shields.io/github/issues/othneildrew/Best-README-Template.svg?style=for-the-badge
[issues-url]: https://github.com/SyedMustafaImam/HPCC-On-VMware-/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=for-the-badge
[license-url]: https://github.com/SyedMustafaImam/HPCC-On-VMware-/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555

[linkedin-url]: https://linkedin.com/in/othneildrew
[product-screenshot]: images/screenshot.png

[linkedin-url-mustafa]: https://linkedin.com/in/syedmustafaimam
[linkedin-url-elliott]: https://www.linkedin.com/in/elliott-joseph-6436411ab/
[linkedin-url-hirdesh]: https://www.linkedin.com/in/hirdeshkumar2407/
[linkedin-url-hurrar]: https://www.linkedin.com/in/syedhurrarhasanrizvi/

[product-screenshot]: images/screenshot.png
