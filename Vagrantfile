Vagrant.configure("2") do |config|
  config.vm.box = "almalinux/9"

  config.vm.network "public_network"

  config.vm.provider :vmware_desktop do |vmware|
    vmware.vmx["ethernet0.pcislotnumber"] = "160"
    vmware.vmx["ethernet1.pcislotnumber"] = "224"
  end

  config.vm.define "k8s-master" do |master|
    master.vm.hostname = "k8s-master"
    
    master.vm.provider "vmware_desktop" do |v|
      v.cpus = 2
      v.memory = 4096
    end
  end

  (1..3).each do |i|
    config.vm.define "k8s-worker-0#{i}" do |worker|
      worker.vm.hostname = "k8s-worker-0#{i}"
      
      worker.vm.provider "vmware_desktop" do |v|
        v.cpus = 2
        v.memory = 4096
      end
    end
  end

  config.vm.define "nfs-server" do |nfs|
    nfs.vm.hostname = "nfs-server"
    
    nfs.vm.provider "vmware_desktop" do |v|
      v.cpus = 2
      v.memory = 2048
    end
  end
end