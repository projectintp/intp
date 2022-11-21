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
    
3 - Install Systemtap:

    $ apt-get install systemtap
    
4 - Install SystemTap dependencies:
    
    $ apt-get install make g++ python gettext libdw-dev
    $ apt-get install intel-cmt-cat
    $ stap-prep

4 - Restart the server after the installation to apply debugging and headers packages:

    $ reboot

5 - Verify the version of the debugging packages (needs to be the same kernel version):

    $ apt list | grep linux-image-$(uname -r)-dbg
    linux-image-5.10.0-14-cloud-amd64-dbg/stable-security,now 5.10.113-1 amd64 [installed]
    
6 - Run the command below to test SYSTEMTAP:

    $ stap -e 'probe begin { log("hello world") exit () }'

After install <b>SYSTEMTAP</b> is possible to execute <b>IntP</b>:

7 - Execute IntP:

    $ stap --suppress-handler-errors -g intp.stp _ApplicationName_

8 - Open a second terminal and execute the command below to see the IntP return:
    
    $ watch -n2 -d cat /proc/systemtap/stap_*/intestbench
