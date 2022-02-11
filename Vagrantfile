IMAGE_2004 = "ubuntu/focal64"


ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|
  NodeType1 = 2
  (1..NodeType1).each do |type1_id|
    config.vm.define "type1#{type1_id}" do |type1_vm|
    
      type1_vm.vm.box = IMAGE_2004
      type1_vm.vm.hostname = "type1#{type1_id}.aruniq.ir"
      type1_vm.vm.network "public_network", ip: "192.168.1.21#{type1_id}"
      type1_vm.vm.provider "virtualbox" do |v|  
        v.name = "type1#{type1_id}"
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
