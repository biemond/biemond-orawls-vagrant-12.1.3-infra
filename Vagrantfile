# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "jrf2admin2" , primary: true do |jrf2admin2|

    jrf2admin2.vm.box = "centos-6.5-x86_64"
    jrf2admin2.vm.box_url = "https://dl.dropboxusercontent.com/s/np39xdpw05wfmv4/centos-6.5-x86_64.box"

    jrf2admin2.vm.hostname = "jrf2admin2.example.com"
    jrf2admin2.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777","fmode=777"]
    jrf2admin2.vm.synced_folder "/Users/edwin/software", "/software"

    jrf2admin2.vm.network :private_network, ip: "10.10.10.21"
  
    jrf2admin2.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "2548"]
      vb.customize ["modifyvm", :id, "--name"  , "jrf2admin2"]
      vb.customize ["modifyvm", :id, "--cpus"  , 2]
    end
  
    jrf2admin2.vm.provision :shell, :inline => "ln -sf /vagrant/puppet/hiera.yaml /etc/puppet/hiera.yaml;rm -rf /etc/puppet/modules;ln -sf /vagrant/puppet/modules /etc/puppet/modules"
    
    jrf2admin2.vm.provision :puppet do |puppet|
      puppet.manifests_path    = "puppet/manifests"
      puppet.module_path       = "puppet/modules"
      puppet.manifest_file     = "site.pp"
      puppet.options           = "--verbose --hiera_config /vagrant/puppet/hiera.yaml"
  
      puppet.facter = {
        "environment"    => "development",
        "vm_type"        => "vagrant",
      }
      
    end
  
  end

  config.vm.define "wlsdb" , primary: true do |wlsdb|
    #wlsdb.vm.box = "centos-6.5-x86_64"
    #wlsdb.vm.box_url = "https://dl.dropboxusercontent.com/s/np39xdpw05wfmv4/centos-6.5-x86_64.box"

    wlsdb.vm.box = "centos-7.0-x86_64"
    wlsdb.vm.box_url = "https://dl.dropboxusercontent.com/s/2w877odvrzj6v9x/centos-7.0-x86_64.box"

    wlsdb.vm.hostname = "wlsdb.example.com"
    wlsdb.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777","fmode=777"]
    wlsdb.vm.synced_folder "/Users/edwin/software", "/software"

    wlsdb.vm.network :private_network, ip: "10.10.10.5"
  
    wlsdb.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm"     , :id, "--memory", "2548"]
      vb.customize ["modifyvm"     , :id, "--name"  , "wlsdb"]
      vb.customize ["modifyvm"     , :id, "--cpus"  , 2]
    end

  
    wlsdb.vm.provision :shell, :inline => "ln -sf /vagrant/puppet/hiera.yaml /etc/puppet/hiera.yaml;rm -rf /etc/puppet/modules;ln -sf /vagrant/puppet/modules /etc/puppet/modules"
    
    wlsdb.vm.provision :puppet do |puppet|
      puppet.manifests_path    = "puppet/manifests"
      puppet.module_path       = "puppet/modules"
      puppet.manifest_file     = "db.pp"
      puppet.options           = [
                                  '--verbose',
                                  '--report',
#                                  '--debug',
                                  '--parser future',
                                  '--strict_variables',
                                  '--hiera_config /vagrant/puppet/hiera.yaml'
                                 ]

  
      puppet.facter = {
        "environment" => "development",
        "vm_type"     => "vagrant",
      }
      
    end
  
  end

end
