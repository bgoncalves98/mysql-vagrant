$script_mysql = <<-SCRIPT
  apt-get update && \
  apt-get install -y mysql-server-5.7 && \
  mysql < /vagrant/mysql/query.sql
  cat /vagrant/mysql/mysqld.cnf > /etc/mysql/mysql.conf.d/mysqld.cnf && \
  service mysql restart
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.network "forwarded_port", guest: 3306, host: 3306, host_ip: "127.0.0.1"
  config.vm.define "mysql-vagrant" do |vagrantmysqlserver|

    vagrantmysqlserver.vm.provider "virtualbox" do |vb|
      vb.name = "mysql-vagrant"
    end

    vagrantmysqlserver.vm.provision "shell", inline: $script_mysql
  end
end