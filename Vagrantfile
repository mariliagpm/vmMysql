  
$script_mysql = <<-SCRIPT
  apt-get update && \
  apt-get install -y mysql-server-5.7 && \
  mysql < /vagrant/mysql/script/user.sql && \
  cat /vagrant/mysql/mysqld.cnf > /etc/mysql/mysql.conf.d/mysqld.cnf && \
  service mysql restart
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end

  config.vm.define "mysqlserver" do |mysqlserver|
    mysqlserver.vm.network "forwarded_port", guest: 3306, host: 3306, ip: "10.80.4.10",host_ip: "127.0.0.1"

    mysqlserver.vm.provider "virtualbox" do |vb|
      vb.name = "mysqlserverDatabase"
    end

    mysqlserver.vm.provision "shell", inline: $script_mysql
  end
config.vm.provision :shell, :inline => "sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config; sudo systemctl restart sshd;", run: "always"
end


