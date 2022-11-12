Vagrant.configure("2") do |config|

  config.vm.box = "debian/bullseye64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.define "wordpress" do |m|
    m.vm.network "private_network", ip: "172.17.177.43"


    m.vm.provision "shell", inline: <<-'SHELL'
        mkdir -p /root/.ssh
        cp /vagrant/keys/id_rsa /root/.ssh/id_rsa
        cp /vagrant/keys/id_rsa.pub /root/.ssh/authorized_keys
        chmod 600 /root/.ssh/id_rsa
        sed -Ei 's,#PermitRootLogin prohibit-password,PermitRootLogin yes,' /etc/ssh/sshd_config
        sed -Ei 's,#?PasswordAuthentication .*,PasswordAuthentication yes,' /etc/ssh/sshd_config
        systemctl restart sshd
        > /etc/udev/rules.d/70-persistent-net.rules

        SHELL
  end


end
