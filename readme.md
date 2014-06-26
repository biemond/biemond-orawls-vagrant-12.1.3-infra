#WebLogic 12.1.3 infra (JRF) cluster

##Details
- CentOS 6.5 vagrant box
- Puppet 3.5.0
- Vagrant >= 1.41
- Oracle Virtualbox >= 4.3.6 

Download & Add the all the Oracle binaries to /software

edit Vagrantfile and update the software share to your own local folder
- wlsdb.vm.synced_folder "/Users/edwin/software", "/software"
- jrf2admin2.vm.synced_folder "/Users/edwin/software", "/software"

Vagrant boxes
- vagrant up wlsdb
- vagrant up jrf2admin2

## Database
- wlsdb 10.10.10.5, 11.2.0.4

###software
- Oracle Database 11.2.0.4 Linux
- 1395582860 Aug 31 16:21 p13390677_112040_Linux-x86-64_1of7.zip
- 1151304589 Aug 31 16:22 p13390677_112040_Linux-x86-64_2of7.zip

## Middleware

### Cluster with 1 node
- jrf2admin2 10.10.10.21, WebLogic 12.1.3 with Infra ( JRF, ADF ) requires RCU

###software
- JDK 1.7u51 jdk-7u51-linux-x64.tar.gz
- JDK 7 JCE policy UnlimitedJCEPolicyJDK7.zip  
- fmw_12.1.3.0.0_infrastructure.jar
