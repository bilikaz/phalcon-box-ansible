# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

module OS
  def OS.windows?
    (/cygwin|mswin|mingw|bccwin|wince|emx/ =~ RUBY_PLATFORM) != nil
  end
  def OS.mac?
    (/darwin/ =~ RUBY_PLATFORM) != nil
  end
  def OS.unix?
    !OS.windows?
  end
  def OS.linux?
    OS.unix? and not OS.mac?
  end
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "laravel/homestead"
  config.vm.box_version = "6.1.0"

  config.vm.define 'default' do |default|
    default.vm.hostname = 'development'
  end

  config.vm.network "forwarded_port", guest: 80, host: 8888
  config.vm.network "forwarded_port", guest: 3306, host: 3308
  config.vm.network "forwarded_port", guest: 22, host: 2200, id: "ssh"

  config.vm.network "private_network", ip: "192.168.10.10"

  config.ssh.forward_agent = true

  config.vm.synced_folder ".", "/vagrant", disabled: true

  if OS.mac?
    config.vm.synced_folder "../",  "/var/www", type: "nfs",
      mount_options: ['rw', 'vers=3', 'tcp', 'fsc', 'actimeo=2'],
      bsd__nfs_options: ["maproot=0:0"]
  else
    if OS.linux?
      config.vm.synced_folder "../", "/var/www", type: "nfs"
    end
  end

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

end
