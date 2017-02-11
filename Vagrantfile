# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # select Ubuntu 16.04 image
  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
  end

  # setup port forwarding for elasticsearch
  config.vm.network "forwarded_port", guest: 9200, host: 9200
  # setup port forwarding for kibana
  config.vm.network "forwarded_port", guest: 5601, host: 5601

  # install elastic search
  config.vm.provision "shell", inline: <<-SHELL
     
     # install Oracle Java 8
     add-apt-repository ppa:webupd8team/java
     echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
     apt-get update && apt-get install -y oracle-java8-installer apt-transport-https
     
     # setup elastic's apt repo
     wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
     if ! grep "deb https://artifacts.elastic.co/packages/5.x/apt stable main" /etc/apt/sources.list.d/elastic-5.x.list > /dev/null; then
        echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | tee -a /etc/apt/sources.list.d/elastic-5.x.list
     fi
     
     # install elasticsearch
     apt-get update && apt-get install -y elasticsearch
     /bin/systemctl daemon-reload
     /bin/systemctl enable elasticsearch.service
     #FIXME should be re-runnable
     if ! grep "network.host: 0.0.0.0" /etc/elasticsearch/elasticsearch.yml > /dev/null; then
        echo network.host: 0.0.0.0 >> /etc/elasticsearch/elasticsearch.yml
     fi
     if ! grep "ES_JAVA_OPTS= -Xms512m -Xmx512m" /etc/default/elasticsearch > /dev/null; then
        echo ES_JAVA_OPTS= -Xms512m -Xmx512m >> /etc/default/elasticsearch
     fi
     service elasticsearch start
     
     # install kibana
     apt-get install -y kibana
     /bin/systemctl daemon-reload
     /bin/systemctl enable kibana.service
     if ! grep "server.host: 0.0.0.0" /etc/kibana/kibana.yml > /dev/null; then
         echo server.host: 0.0.0.0 >> /etc/kibana/kibana.yml
     fi
     service kibana start
   SHELL
end
