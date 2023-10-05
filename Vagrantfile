Vagrant.configure("2") do |config|
  # Máquina 01 (Cliente)
  config.vm.define "cliente" do |cliente|
    cliente.vm.box = "ubuntu/trusty64"
    cliente.vm.network "private_network", type: "dhcp"
    cliente.vm.hostname = "daniel-lucivando-client"

    # Configuração de rede privada com IP fixo
    cliente.vm.network "private_network", type: "static", ip: "192.168.56.11"

    # Executa um shell script para instalar pacotes
    cliente.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y curl vim htop
    SHELL
  end

  # Máquina 02 (Server)
  config.vm.define "server" do |server|
    server.vm.box = "ubuntu/trusty64"
    server.vm.network "private_network", type: "dhcp"
    server.vm.hostname = "daniel-lucivando-server"

    # Configuração de rede privada com IP fixo
    server.vm.network "private_network", type: "static", ip: "192.168.56.12"

    # Executa um shell script para instalar pacotes
    server.vm.provision "shell", inline: <<-SHELL
      yum install -y docker git wget
      systemctl start docker
      systemctl enable docker
      curl -fsSL https://get.docker.com -o get-docker.sh
      sh get-docker.sh
      wget https://github.com/docker/compose/releases/download/1.29.2/docker-compose-Linux-x86_64 -O /usr/local/bin/docker-compose
      chmod +x /usr/local/bin/docker-compose
    SHELL

    # Defina limites de CPU e memória
    server.vm.provider "virtualbox" do |vb|
      vb.memory = 1024 # 1GB de memória
      vb.cpus = 2      # 2 CPUs
    end
  end
end