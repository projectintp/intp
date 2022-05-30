# How to install IntP

Assuming that apt-get package is installed in the system, these packages can be installed with. Make sure to install the required kernel information packages before using IntP:

$ sudo apt-get install linux-image-4.4.0-75-generic

$ sudo apt-get install fdutils linux-source-4.4.0 linux-headers-4.4.0-75-generic

The debug symbols are required to solve this problem. You can install the symbols as followed:

$ echo "deb http://ddebs.ubuntu.com \$(lsb\_release -cs) main restricted universe multiverse
deb http://ddebs.ubuntu.com \$(lsb\_release -cs)-updates main restricted universe multiverse
deb http://ddebs.ubuntu.com \$(lsb\_release -cs)-proposed main restricted universe multivers'' |  sudo tee -a /etc/apt/sources.list.d/ddebs.list

$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 428D7C01 C8CAB6595FDFF622

$ sudo apt-get update

$ sudo apt-get install linux-image-4.4.0-75-generic-dbgsym

Installing make, g++, python and some more packages (gettext and libdw-dev):

$ sudo apt-get install make g++ python gettext libdw-dev


# Downloading and installing systemtap 3.1:

$ wget https://sourceware.org/systemtap/ftp/releases/systemtap-3.1.tar.gz

$ tar -xvzf systemtap-3.1.tar.gz

$ cd systemtap-3.1

$ sudo su

 ./configure

 make

 make install

 rm -rf /root/.systemstap/*.*

 reboot (Restarting the computer is recommended to execute IntP)


In order to test the whole installation packages:

 stap  -e 'probe begin{ printf("Hello, World!"); exit()}'


# How to use IntP


IntP is a probing tool that allows users to monitor the activities of the computer system with more detail. It is important to note that IntP runs in kernel-space, so it is possible to provide analysis over a specific application in fine detail. Assuming the user or programmer wants to monitor a specific application with a higher level of details. IntP works such as a listener, which hears only the chosen application and collects all the interactions made by the application over the hardware. The execution of IntP is similar to other tools like top or netstat, but there is a significant difference between them, IntP does not work with just only one command. To execute IntP, at least two commands have to be executed and consequently two shell terminals have to be used. The command which was used for monitoring an application with IntP is:


 stap --suppress-handler-errors -g intp.stp ApplicationName


To take IntP return it is needed to open a second shell terminal and type another command, as follows:


 watch -n2 -d cat /proc/systemtap/stap_*/intestbench
