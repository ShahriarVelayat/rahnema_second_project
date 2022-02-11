IMAGE_2004 = "ubuntu/focal64"

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|
  VmCounts = 2
  (1..VmCounts).each do |vm_id|
    config.vm.define "vm#{vm_id}" do |vm_no|
    
      vm_no.vm.box = IMAGE_2004
      vm_no.vm.hostname = "vm#{vm_id}.aruniq.ir"
      vm_no.vm.network "public_network", ip: "192.168.1.21#{vm_id}"
      vm_no.vm.provider "virtualbox" do |v|  
        v.name = "vm#{vm_id}"
        v.memory = 2048
        v.cpus = 2
      end
    end
  end
config.vm.provision "shell" do |s|
  ssh_pub_key = File.readlines("/home/shahriar/Desktop/shahriar_main.pub").first.strip
  s.inline = <<-SHELL
    echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
    echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
  SHELL
end
end
