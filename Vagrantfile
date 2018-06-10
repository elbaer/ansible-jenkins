$sshscript = <<SCRIPT
sudo chmod 600 .ssh/id_rsa
sudo chmod 644 .ssh/authorized_keys
sudo cat .ssh/id_rsa_pub >> .ssh/authorized_keys
SCRIPT

nodes = [
  { :hostname => 'jenkinsmaster', :ip => '192.168.36.10', :box => 'centos/7', :ram => 1024 },
  { :hostname => 'dockerslave',   :ip => '192.168.36.11', :box => 'centos/7' },
  { :hostname => 'javaslave',     :ip => '192.168.36.12', :box => 'centos/7' }
]

Vagrant.configure("2") do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      nodeconfig.vm.box = node[:box]
      nodeconfig.vm.hostname = node[:hostname] + ".box"
      nodeconfig.vm.network :private_network, ip: node[:ip]
      nodeconfig.vm.provision "file", source: "ssh-keys/id_rsa", destination: ".ssh/id_rsa"
      nodeconfig.vm.provision "file", source: "ssh-keys/id_rsa.pub", destination: ".ssh/id_rsa_pub"
      nodeconfig.vm.provision "shell", inline: $sshscript
      nodeconfig.vm.provider :libvirt do |vb|
        vb.memory = node[:ram] ? node[:ram] : 512;
      end
      nodeconfig.vm.provider :virtualbox do |vb|
        vb.memory = node[:ram] ? node[:ram] : 512;
      end
    end
  end
  
  config.vm.provision :shell, inline: "yum -y -q install python java"
end