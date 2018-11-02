
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |vb|
     vb.gui = true
     vb.memory = "512"
     vb.cpus = 1
  end

  $num_instances = 3

  config.vm.box_check_update = false

  (1..$num_instances).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.box = "centos/7"
      node.vm.network "private_network", ip: "172.17.9.10#{i}"
      node.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)", auto_config: true
      config.vm.hostname = "elk-node#{i}"
      node.vm.provision "shell" do |s|
        s.inline = <<-SHELL
          echo "Install OpenJDK 8"
          sudo yum install -y java-1.8.0-openjdk-devel
          java -version

          echo "Install Elasticsearch"
          sudo rpm --import http://packages.elastic.co/GPG-KEY-elasticsearch
          sudo cp /vagrant/repos/elasticsearch.repo /etc/yum.repos.d/
          sudo yum -y install elasticsearch
          sudo cp /vagrant/confs/elasticsearch/node#{i}.yaml /etc/elasticsearch/elasticsearch.yml
          sudo systemctl start elasticsearch
          sudo systemctl enable elasticsearch
          if [[ $1 -eq 1 ]];then
            echo "Install Kibana"
            sudo cp /vagrant/repos/kibana.repo /etc/yum.repos.d/kibana.repo
            sudo yum -y install kibana
            sudo cp /vagrant/confs/kibana.yaml /etc/kibana/kibana.yml
            sudo systemctl start kibana
            sudo systemctl enable kibana
          fi
          SHELL
          s.args = [i]
        end
      end
  end
end
