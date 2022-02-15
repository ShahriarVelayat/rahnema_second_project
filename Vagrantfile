
VAGRANTFILE_API_VERSION = "2"

cluster = {
  "master" => { :ip => "192.168.50.13", :cpus => 1, :mem => 1024 },
  "slave" => { :ip => "192.168.50.14", :cpus => 1, :mem => 1024 },
  "monitoring" => { :ip => "192.168.50.15", :cpus => 1, :mem => 1024 },
}
 
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  cluster.each_with_index do |(hostname, info), index|

    config.vm.define hostname do |cfg|
      cfg.vm.provider :virtualbox do |vb, override|
        config.vm.box = "ubuntu/focal64"
        override.vm.network :private_network, ip: "#{info[:ip]}"
        override.vm.hostname = hostname
        vb.name = hostname
        vb.customize ["modifyvm", :id, "--memory", info[:mem], "--cpus", info[:cpus], "--hwvirtex", "on"]
      end # end provider
    end # end config
    config.vm.provision "shell" do |s|
      ssh_pub_key = File.readlines("shahriar_main_without_pass.pub").first.strip
      s.inline = <<-SHELL
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
      SHELL
    end
  end # end cluster
end