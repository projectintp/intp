# IntP INSTALLATION GUIDE

<b>IntP</b> is based in <b>SYSTEMTAP</b>, to install <b>SYSTEMTAP</b> and execute <b>IntP</b> follows the steps below:

To install SYSTEMTAP first is necessary to install "kerneldebug-info" packages, for this:

1 - Indentify what is the version of the kernel in use:

    $ uname -a
    5.10.130-118.517.amzn2.x86_64
    
In my case is the version 5.10.130.

2 - Enable "debuginfo repository" (this repository is unabled by default):

    $ yum repolist disabled
    Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
    repo id                                                           repo name                                                                   
    amzn2-core-debuginfo/2/x86_64                                     Amazon Linux 2 core repository - debuginfo packages                         
    amzn2-core-source/2                                               Amazon Linux 2 core repository - source packages                            
    amzn2extra-docker-debuginfo/2/x86_64                              Amazon Extras debuginfo repo for docker                                     
    amzn2extra-docker-source/2                                        Amazon Extras source repo for docker                                        
    amzn2extra-kernel-5.10-debuginfo/2/x86_64                         Amazon Extras debuginfo repo for kernel-5.10                                
    amzn2extra-kernel-5.10-source/2                                   Amazon Extras source repo for kernel-5.10
    
    $ yum-config-manager --enable "Amazon Extras debuginfo repo for kernel-5.10"
    
The version of debuginfo needs to be the same of the kernel (in this example 5.10).
    
3 - Now is possible to find the debuginfo packages and install:

    $ yum search kernel | grep ^kernel-debuginfo
    kernel-debuginfo.x86_64 : Debug information for package kernel
    kernel-debuginfo-common-x86_64.x86_64 : Kernel source files used by
    
    $ yum -y install kernel-debuginfo kernel kernel-devel

4 - Restart the server after the installation to apply the new kernel:

    $ init 6

5 - Verify the new kernel version:

    $ uname -a
    5.10.135-122.509.amzn2.x86_64
    
In my case the new kernel version is 5.10.135.
    
6 - Verify if the version of debuginfo is the same version of the kernel (5.10.135):

    $ rpm -qa | grep ^kernel
    kernel-debuginfo-common-x86_64-5.10.135-122.509.amzn2.x86_64
    kernel-devel-5.10.135-122.509.amzn2.x86_64
    kernel-5.10.130-118.517.amzn2.x86_64
    kernel-tools-5.10.130-118.517.amzn2.x86_64
    kernel-debuginfo-5.10.135-122.509.amzn2.x86_64
    kernel-headers-5.10.135-122.509.amzn2.x86_64
    kernel-5.10.135-122.509.amzn2.x86_64

7 - Install SYSTEMTAP packages:

    $ yum list systemtap*
    Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
    Installed Packages
    systemtap-runtime.x86_64                                                   4.5-1.amzn2.0.1                                          installed 
    Available Packages
    systemtap.x86_64                                                           4.5-1.amzn2.0.1                                          amzn2-core
    systemtap-client.x86_64                                                    4.5-1.amzn2.0.1                                          amzn2-core
    systemtap-devel.x86_64                                                     4.5-1.amzn2.0.1                                          amzn2-core
    systemtap-initscript.x86_64                                                4.5-1.amzn2.0.1                                          amzn2-core
    systemtap-runtime-java.x86_64                                              4.5-1.amzn2.0.1                                          amzn2-core
    systemtap-runtime-python2.x86_64                                           4.5-1.amzn2.0.1                                          amzn2-core
    systemtap-runtime-virtguest.x86_64                                         4.5-1.amzn2.0.1                                          amzn2-core
    systemtap-runtime-virthost.x86_64                                          4.5-1.amzn2.0.1                                          amzn2-core
    systemtap-sdt-devel.x86_64                                                 4.5-1.amzn2.0.1                                          amzn2-core
    systemtap-server.x86_64                                                    4.5-1.amzn2.0.1                                          amzn2-core
    systemtap-testsuite.x86_64                                                 4.5-1.amzn2.0.1                                          amzn2-core
    
    $ yum install -y sytemtap
    
8 - Install c++ packages:

    $ yum install -y gcc-c+
    
9 - Run the command below to test SYSTEMTAP:

    $ stap -e 'probe begin { log("hello world") exit () }'

After install <b>SYSTEMTAP</b> is possible to execute <b>IntP</b>:

10 - Execute Intp:

    $ stap --suppress-handler-errors -g intp.stp _ApplicationName_

11 - Open a second terminal and execute the command below to see the IntP return:
    
    $ watch -n2 -d cat /proc/systemtap/stap_*/intestbench
