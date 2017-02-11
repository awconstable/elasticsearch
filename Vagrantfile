# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "forwarded_port", guest: 9200, host: 9200
  # install elastic search
  config.vm.provision "shell", inline: <<-SHELL
     wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
     add-apt-repository ppa:webupd8team/java
     echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
     apt-get update && apt-get install -y oracle-java8-installer apt-transport-https
     echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | tee -a /etc/apt/sources.list.d/elastic-5.x.list
     apt-get update && apt-get install -y elasticsearch
     /bin/systemctl daemon-reload
     /bin/systemctl enable elasticsearch.service
     echo network.host: 0.0.0.0 >> /etc/elasticsearch/elasticsearch.yml
     echo ES_JAVA_OPTS= -Xms512m -Xmx512m >> /etc/default/elasticsearch
     service elasticsearch start
   SHELL
end
