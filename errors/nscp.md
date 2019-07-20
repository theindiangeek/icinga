[root@apachenode7 ~]# yum install https://github.com/mickem/nscp/releases/downlo                                                                ad/0.4.3.143/NSCP-0.4.3.143-1.el7.x86_64.rpm  -y
Loaded plugins: fastestmirror
NSCP-0.4.3.143-1.el7.x86_64.rpm                          |  49 MB     00:06
Examining /var/tmp/yum-root-cbpoGT/NSCP-0.4.3.143-1.el7.x86_64.rpm: nscp-0.4.3.1                                                                43-1.x86_64
Marking /var/tmp/yum-root-cbpoGT/NSCP-0.4.3.143-1.el7.x86_64.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package nscp.x86_64 0:0.4.3.143-1 will be installed
--> Processing Dependency: boost-filesystem for package: nscp-0.4.3.143-1.x86_64
Loading mirror speeds from cached hostfile
 * base: centos.mirrors.estointernet.in
 * extras: centos.mirrors.estointernet.in
 * updates: centos.mirrors.estointernet.in
--> Processing Dependency: protobuf for package: nscp-0.4.3.143-1.x86_64
--> Processing Dependency: libboost_date_time-mt.so.1.53.0()(64bit) for package:                                                                 nscp-0.4.3.143-1.x86_64
--> Processing Dependency: libboost_filesystem-mt.so.1.53.0()(64bit) for package                                                                : nscp-0.4.3.143-1.x86_64
--> Processing Dependency: libboost_python-mt.so.1.53.0()(64bit) for package: ns                                                                cp-0.4.3.143-1.x86_64
--> Processing Dependency: libcryptopp.so.6()(64bit) for package: nscp-0.4.3.143                                                                -1.x86_64
--> Processing Dependency: libprotobuf.so.8()(64bit) for package: nscp-0.4.3.143                                                                -1.x86_64
--> Running transaction check
---> Package boost-date-time.x86_64 0:1.53.0-27.el7 will be installed
---> Package boost-filesystem.x86_64 0:1.53.0-27.el7 will be installed
---> Package boost-python.x86_64 0:1.53.0-27.el7 will be installed
---> Package nscp.x86_64 0:0.4.3.143-1 will be installed
--> Processing Dependency: libcryptopp.so.6()(64bit) for package: nscp-0.4.3.143                                                                -1.x86_64
---> Package protobuf.x86_64 0:2.5.0-8.el7 will be installed
--> Finished Dependency Resolution
Error: Package: nscp-0.4.3.143-1.x86_64 (/NSCP-0.4.3.143-1.el7.x86_64)
           Requires: libcryptopp.so.6()(64bit)
 You could try using --skip-broken to work around the problem
 You could try running: rpm -Va --nofiles --nodigest
[root@apachenode7 ~]# rpm -ivh http://download-ib01.fedoraproject.org/pub/epel/7                                                                /x86_64/Packages/c/cryptopp-5.6.2-10.el7.x86_64.rpm
Retrieving http://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/c/c                                                                ryptopp-5.6.2-10.el7.x86_64.rpm
Preparing...                          ################################# [100%]
Updating / installing...
   1:cryptopp-5.6.2-10.el7            ################################# [100%]
