# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.define :salt do |node|
    node.vm.box = "freebsd/FreeBSD-10.2-STABLE"
    node.vm.hostname = "salt"
    node.ssh.shell = "sh"
    node.vm.base_mac = "080027D14C66"
    node.vm.network "private_network", ip: "192.168.50.4"

    node.vm.provision "shell", inline: <<-SHELL
      mkdir -vp /usr/local/etc/salt
      pkg install -y  py27-pip vim tmux git gcc bash py27-m2crypto py27-pycrypto
      pip install --upgrade pip
      pip install pyzmq PyYAML msgpack-python jinja2 psutil futures tornado
      chsh -s /usr/local/bin/bash vagrant
      chsh -s /usr/local/bin/bash root
    SHELL

    node.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true
    node.vm.synced_folder "~/work/code/salt/", "/root/salt", type: "nfs"
    node.vm.synced_folder "saltstack/srv", "/srv", type: "nfs"
    node.vm.synced_folder "saltstack/etc", "/usr/local/etc/salt", type: "nfs"

    node.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024"]
      vb.customize ["modifyvm", :id, "--cpus", "1"]
      vb.customize ["modifyvm", :id, "--hwvirtex", "on"]
      vb.customize ["modifyvm", :id, "--audio", "none"]
      vb.customize ["modifyvm", :id, "--nictype1", "virtio"]
      vb.customize ["modifyvm", :id, "--nictype2", "virtio"]
    end
  end
end
