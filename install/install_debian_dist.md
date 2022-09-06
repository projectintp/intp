# IntP INSTALLATION GUIDE FOR DEBIAN BASED DISTRIBUTION

<b>IntP</b> is based in <b>SYSTEMTAP</b>, to install <b>SYSTEMTAP</b> and execute <b>IntP</b> follows the steps below:

To install SYSTEMTAP first is necessary to install headers and debugging packages, for this:

1 - Indentify what is the version of the kernel in use:

    $ uname -a
    Debian 5.10.113-1 (2022-04-29) x86_64 GNU/Linux
    
In my case is the version 5.10.113.

2 - Enable "debuginfo repository" (this repository is unabled by default):

    $ tee /etc/apt/sources.list.d/debug.list << EOF
      deb http://deb.debian.org/debian-debug/ $(lsb_release -cs)-debug main
      deb http://deb.debian.org/debian-debug/ $(lsb_release -cs)-proposed-updates-debug main
      EOF
      
    $ apt-get update
    
3 - Now is necessary to install the debugging and headers packages:

    $ apt-get install linux-image-$(uname -r)-dbg
    
    $ apt-get install linux-headers-`uname -r`

4 - Restart the server after the installation to apply debugging and headers packages:

    $ init 6

5 - Verify the version of the debugging packages (needs to be the same kernel version):

    $ apt-get list | grep linux-image-$(uname -r)-dbg
    linux-image-5.10.0-14-cloud-amd64-dbg/stable-security,now 5.10.113-1 amd64 [installed]
    
In my case the kernel version is 5.10.113.

6 - Install SYSTEMTAP packages:

    $ apt-get install -y systemtap
    
7 - Install  make, c++, python, gettext and libdw-dev packages:

    $ apt-get install make g++ python gettext libdw-dev
    
8 - Run the command below to test SYSTEMTAP:

    $ stap -e 'probe begin { log("hello world") exit () }'

After install <b>SYSTEMTAP</b> is possible to execute <b>IntP</b>:

9 - Execute IntP:

    $ stap --suppress-handler-errors -g intp.stp _ApplicationName_

10 - Open a second terminal and execute the command below to see the IntP return:
    
    $ watch -n2 -d cat /proc/systemtap/stap_*/intestbench
