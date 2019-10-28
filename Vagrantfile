Vagrant.configure("2") do |config|

    config.vm.box = "~/virtualbox.box"
  
    config.vm.define "ids-snort" do |machine|
        machine.vm.hostname = "snort"
        machine.vm.network "private_network", ip: "192.168.0.10"
        machine.vm.provision "ansible", playbook: "provision/playbook.yml"
        machine.vm.provision "shell", inline: <<-SHELL
        cd /home/vagrant/snort_src/snort-2.9.15/etc
        cp -avr *.conf *.map *.dtd *.config /etc/snort/
        cd ..
        cp -avr src/dynamic-preprocessors/build/usr/local/lib/snort_dynamicpreprocessor/* /usr/local/lib/snort_dynamicpreprocessor/
        sed -i "s/include \$RULE\_PATH/#include \$RULE\_PATH/" /etc/snort/snort.conf
        SHELL
    end

 #   config.vm.define "ids-suricata" do |machine|
 #       machine.vm.hostname = "suricata"
 #       machine.vm.network "private_network", ip: "192.168.0.20"
 #       machine.vm.provision "ansible", playbook: "provision/playbook.yml"
 #   end
#
#    config.vm.define "ids-zeek" do |machine|
#        machine.vm.hostname = "zeek"
#        machine.vm.network "private_network", ip: "192.168.0.30"
#        machine.vm.provision "shell", inline: <<-SHELL
#        sudo sh -c "echo 'deb http://download.opensuse.org/repositories/security:/zeek/xUbuntu_18.04/ /' > /etc/apt/sources.list.d/security:zeek.list"
#        wget -nv https://download.opensuse.org/repositories/security:zeek/xUbuntu_18.04/Release.key -O Release.key
#        sudo apt-key add - < Release.key
#        sudo apt-get update
#        sudo DEBIAN_FRONTEND=noninteractive apt-get -yq install zeek
#        SHELL
        #machine.vm.provision "ansible", playbook: "provision/playbook.yml"
#    end

end