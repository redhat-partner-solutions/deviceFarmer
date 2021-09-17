Vagrant.configure("2") do |config|
    config.vm.define "stf-build"
    config.vm.box = "generic/rhel8"
    config.vm.provider :libvirt do |libvirt|
      libvirt.cpus = 2
      libvirt.memory = 4096
    end
    config.vm.provision :shell, path: "bootstrap"
end
