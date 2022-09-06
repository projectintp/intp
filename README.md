![image](https://github.com/projectintp/intp/blob/main/img/intp2.png)

IntP is a tool to measure the interference of direct applications in linux operational systems.

Meaning of interference: is the overhead generated in an aplication running in a consolidated environment with other applications due to contention in accessing shared resources.

# How to Install IntP

[Installation Guide - Red Hat Based Distribution](https://github.com/projectintp/intp/blob/main/install/install_redhat_dist.md)

# How to Use IntP

IntP is a probing tool that allows users to monitor the activities of the computer system with more detail. It is important to note that IntP runs in kernel-space, so it is possible to provide analysis over a specific application in fine detail. Assuming the user or programmer wants to monitor a specific application with a higher level of details. IntP works such as a listener, which hears only the chosen application and collects all the interactions made by the application over the hardware. The execution of IntP is similar to other tools like top or netstat, but there is a significant difference between them, IntP does not work with just only one command. To execute IntP, at least two commands have to be executed and consequently two shell terminals have to be used. The command which was used for monitoring an application with IntP is:


 stap --suppress-handler-errors -g intp.stp ApplicationName


To take IntP return it is needed to open a second shell terminal and type another command, as follows:


 watch -n2 -d cat /proc/systemtap/stap_*/intestbench

# Contributors
[@mclsylva](https://github.com/mclsylva)

[@superflit](https://github.com/superflit)

