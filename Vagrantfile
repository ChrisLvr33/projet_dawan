Vagrant.configure("2") do |config|

  # NS1
  config.vm.define "ns1" do |ns1|
    ns1.vm.box = "debian/bullseye64"
    ns1.vm.hostname = "ns1.lvr.org"
    ns1.vm.network "private_network", ip: "192.168.56.10"
    ns1.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = "1"
    end

    ns1.vm.provision :ansible do |ansible|
      ansible.verbose = "v"
      ansible.limit = "all"
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "ansible-dns/playbook_roles-dns.yml"
      ansible.inventory_path = "ansible-dns/inventaires"
      ansible.config_file = "ansible-dns/ansible.cfg"
      ansible.become = true
    end
  end

  # MAIL1
  config.vm.define "mail1" do |mail1|
    mail1.vm.box = "debian/bullseye64"
    mail1.vm.hostname = "mail1.lvr.org"
    mail1.vm.network "private_network", ip: "192.168.56.20"
    mail1.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = "1"
    end

    mail1.vm.provision :ansible do |ansible|
      ansible.verbose = "v"
      ansible.limit = "all"
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "ansible-mail/playbook_roles-postfix.yml"
      ansible.inventory_path = "ansible-mail/inventaires"
      ansible.config_file = "ansible-mail/ansible.cfg"
      ansible.become = true
    end
  end

  # WEBMAIL
  config.vm.define "wmail" do |wmail|
    wmail.vm.box = "debian/bullseye64"
    wmail.vm.hostname = "webmail.lvr.org"
    wmail.vm.network "private_network", ip: "192.168.56.30"
    wmail.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = "1"
    end

    wmail.vm.provision :ansible do |ansible|
      ansible.verbose = "v"
      ansible.limit = "all"
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "ansible-webmail/playbook-webmail.yml"
      ansible.inventory_path = "ansible-webmail/inventaires"
      ansible.config_file = "ansible-webmail/ansible.cfg"
      ansible.become = true
    end
  end
end
