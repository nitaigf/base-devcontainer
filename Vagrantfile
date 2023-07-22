# -*- mode: ruby -*-
# vi: set ft=ruby :

# vagrant-vbguest automatically installs the host's VirtualBox Guest Additions on the guest system.
# vagrant plugin install vagrant-vbguest

# vagrant plugin install vagrant-dotenv
# require 'vagrant/dotenv'
# --
# EXEMPLO .ENV
# Conteúdo do arquivo .env
# AMBIENTE=producao
# --

Vagrant.configure("2") do |config|
  # Carrega as variáveis do .env
  # config.env.enable
  # config.dotenv.load
  # config.vm.box = ENV['VAGRANT_BOX_NAME']
  config.vm.box = "debian/bullseye64"
  # config.vm.box_check_update = false

  # # Configuração para o ambiente de desenvolvimento
  # if ENV['AMBIENTE'] == 'desenvolvimento'
  #   config.vm.box = "ubuntu/bionic64"
  #   # Adicione aqui outras configurações específicas para o ambiente de desenvolvimento
  # end

  # # Configuração para o ambiente de produção
  # if ENV['AMBIENTE'] == 'producao'
  #   config.vm.box = "hashicorp/precise64"
  #   # Adicione aqui outras configurações específicas para o ambiente de produção
  # end

  # config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 80, host: 9080
  config.vm.network "forwarded_port", guest: 81, host: 9081
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 4200, host: 4280
  config.vm.network "forwarded_port", guest: 4000, host: 4000
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 8000, host: 8000
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"

  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder "./node-front", "/app/node-front"
  config.vm.synced_folder "./node-back", "/app/node-back"
  config.vm.synced_folder "./python-back", "/app/python-back"
  config.vm.synced_folder "./ruby-back", "/app/ruby-back"
  config.vm.synced_folder "./java-back", "/app/java-back"
  config.vm.synced_folder "./dotnet-back", "/app/dotnet-back"
  config.vm.synced_folder "./php-back", "/app/php-back"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
  end

  config.vm.provision "shell", inline: <<-SHELL
    # Instalando o git e demais pacotes
    sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get install -y --fix-missing git gpg curl wget build-essential libssl-dev libffi-dev zlib1g-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common apt-transport-https gnupg2 ca-certificates libc6-dev tzdata libgdbm-dev libncurses5-dev automake libtool bison unzip

    # Instalando as bibliotecas dos bancos de dados
    sudo apt-get update && sudo apt-get install -y libsqlite3-dev sqlite3 libpq-dev firebird-dev default-libmysqlclient-dev freetds-dev

    # Instalando o asdf
    git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.12.0
    echo ". $HOME/.asdf/asdf.sh" >> ~/.profile
    echo ". $HOME/.asdf/completions/asdf.bash" >> ~/.profile
    echo 'legacy_version_file = yes' >> ~/.asdfrc
    # exec $SHELL
    . ~/.profile

    # Instalação do Python
    # asdf plugin add python https://github.com/danhper/asdf-python.git
    # asdf install python latest
    # asdf global python latest
    # python -V && pip -V

    # Instalação do NodeJS
    # asdf plugin add nodejs https://github.com/asdf-vm/asdf-nodejs.git
    # asdf install nodejs latest
    # asdf global nodejs latest
    # npm i -g npm @angular/cli @nestjs/cli
    # node -v && npm -v
    # ng version && nest -v

    # Instalação do Ruby
    # asdf plugin add ruby https://github.com/asdf-vm/asdf-ruby.git
    # asdf install ruby latest
    # asdf global ruby latest
    # gem install bundler rails
    # gem update --system 3.4.17
    # ruby -v && bundler -v && rails -v

    # Instalação do Apache 2, Nginx e PHP
    # asdf plugin add php https://github.com/asdf-community/asdf-php.git
    # asdf install php latest
    # asdf global php latest
    # php -v & apache2 -v && nginx -v
  SHELL

  #### Arrumar para funcionar com Vagrant Multimachine
  #https://developer.hashicorp.com/vagrant/docs/multi-machine

  # # VM NODE-FRONT
  # config.vm.define "node-front", primary: true do |nf|
  #   nf.vm.box = "debian/bullseye64"
  #   nf.vm.synced_folder "./node-front", "/app/node-front"
  #   nf.vm.network "forwarded_port", guest: 4200, host: 4200

  #   nf.vm.provider "virtualbox" do |vb|
  #     vb.gui = false
  #     vb.memory = "2048"
  #   end

  #   nf.vm.provision "shell", inline: <<-SHELL
  #     # Instalando o git e demais pacotes
  #     sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get install -y --fix-missing git gpg curl wget build-essential libssl-dev libffi-dev zlib1g-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common apt-transport-https gnupg2 ca-certificates libc6-dev tzdata libgdbm-dev libncurses5-dev automake libtool bison unzip

  #     # Instalando as bibliotecas dos bancos de dados
  #     sudo apt-get update && sudo apt-get install -y libsqlite3-dev sqlite3 libpq-dev firebird-dev default-libmysqlclient-dev freetds-dev

  #     # Instalação do NodeJS
  #     sudo curl -fsSL https://deb.nodesource.com/setup_18.x | sh -
  #     sudo apt-get update && sudo apt-get install -y nodejs
  #     sudo npm i -g npm @angular/cli
  #     # node -v && npm -v
  #     # ng version && nest -v
  #   SHELL
  # end

  # # VM-NODE-BACK
  # config.vm.define "node-back" do |nb|
  #   nb.vm.box = "debian/bullseye64"
  #   nb.vm.synced_folder "./node-back", "/app/node-back"
  #   nb.vm.network "forwarded_port", guest: 4200, host: 4200

  #   nb.vm.provider "virtualbox" do |vb|
  #     vb.gui = false
  #     vb.memory = "2048"
  #   end

  #   nb.vm.provision "shell", inline: <<-SHELL
  #     # Instalando o git e demais pacotes
  #     sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get install -y --fix-missing git gpg curl wget build-essential libssl-dev libffi-dev zlib1g-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common apt-transport-https gnupg2 ca-certificates libc6-dev tzdata libgdbm-dev libncurses5-dev automake libtool bison unzip

  #     # Instalando as bibliotecas dos bancos de dados
  #     sudo apt-get update && sudo apt-get install -y libsqlite3-dev sqlite3 libpq-dev firebird-dev default-libmysqlclient-dev freetds-dev

  #     # Instalação do NodeJS
  #     sudo curl -fsSL https://deb.nodesource.com/setup_18.x | sh -
  #     sudo apt-get update && sudo apt-get install -y nodejs
  #     sudo npm i -g npm @nestjs/cli
  #     # node -v && npm -v
  #     # ng version && nest -v
  #   SHELL
  # end

  # # VM PYTHON-BACK
  # config.vm.define "python-back" do |pb|
  #   pb.vm.box = "debian/bullseye64"
  #   pb.vm.synced_folder "./python-back", "/app/python-back"
  #   pb.vm.network "forwarded_port", guest: 8000, host: 8000

  #   pb.vm.provider "virtualbox" do |vb|
  #     vb.gui = false
  #     vb.memory = "2048"
  #   end

  #   pb.vm.provision "shell", inline: <<-SHELL
  #     # Instalando o git e demais pacotes
  #     sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get install -y --fix-missing git gpg curl wget build-essential libssl-dev libffi-dev zlib1g-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common apt-transport-https gnupg2 ca-certificates libc6-dev tzdata libgdbm-dev libncurses5-dev automake libtool bison unzip

  #     # Instalando as bibliotecas dos bancos de dados
  #     sudo apt-get update && sudo apt-get install -y libsqlite3-dev sqlite3 libpq-dev firebird-dev default-libmysqlclient-dev freetds-dev

  #     # Instalação do Python
  #     sudo apt-get update && sudo apt-get install -y dirmngr gawk
  #     sudo apt-get install -y python python3 python3-pip python3-dev python3-venv
  #     # python -V && pip -V
  #   SHELL
  # end

  # # VM RUBY-BACK
  # config.vm.define "ruby-back" do |rb|
  #   rb.vm.box = "debian/bullseye64"
  #   rb.vm.synced_folder "./ruby-back", "/app/ruby-back"
  #   rb.vm.network "forwarded_port", guest: 3000, host: 3000

  #   rb.vm.provider "virtualbox" do |vb|
  #     vb.gui = false
  #     vb.memory = "2048"
  #   end

  #   rb.vm.provision "shell", inline: <<-SHELL
  #     # Instalando o git e demais pacotes
  #     sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get install -y --fix-missing git gpg curl wget build-essential libssl-dev libffi-dev zlib1g-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common apt-transport-https gnupg2 ca-certificates libc6-dev tzdata libgdbm-dev libncurses5-dev automake libtool bison unzip

  #     # Instalando as bibliotecas dos bancos de dados
  #     sudo apt-get update && sudo apt-get install -y libsqlite3-dev sqlite3 libpq-dev firebird-dev default-libmysqlclient-dev freetds-dev

  #     # Instalação do Ruby
  #     sudo apt-get update && sudo apt-get install -y ruby-full
  #     sudo gem install bundler rails
  #     # gem update --system 3.4.17
  #     # ruby -v && bundler -v && rails -v
  #   SHELL
  # end

  # VM JAVA-BACK
  # config.vm.define "java-back" do |jb|
  #   jb.vm.box = "debian/bullseye64"
  #   jb.vm.synced_folder "./java-back", "/app/java-back"
  # end

  # VM DOTNET-BACK
  # config.vm.define "dotnet-back" do |dotb|
  #   dotb.vm.box = "debian/bullseye64"
  #   dotb.vm.synced_folder "./dotnet-back", "/app/dotnet-back"
  # end

  # # VM PHP-BACK - (+Apache2, + Nginx)
  # config.vm.define "php-back" do |panb|
  #   panb.vm.box = "debian/bullseye64"
  #   panb.vm.synced_folder "./php-back", "/var/www/html/php-back"
  #   panb.vm.network "forwarded_port", guest: 8080, host: 8090
  #   panb.vm.network "forwarded_port", guest: 80, host: 8080
  #   panb.vm.network "forwarded_port", guest: 81, host: 8081

  #   panb.vm.provision "shell", inline: <<-SHELL
  #     # Instalando o git e demais pacotes
  #     sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get install -y --fix-missing git gpg curl wget build-essential libssl-dev libffi-dev zlib1g-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common apt-transport-https gnupg2 ca-certificates libc6-dev tzdata libgdbm-dev libncurses5-dev automake libtool bison unzip

  #     # Instalando as bibliotecas dos bancos de dados
  #     sudo apt-get update && sudo apt-get install -y libsqlite3-dev sqlite3 libpq-dev firebird-dev default-libmysqlclient-dev freetds-dev

  #     # Instalação do Apache 2, Nginx e PHP
  #     sudo apt-get update
      
  #     # - Instalação do Apache2
  #     sudo apt-get install -y apache2
  #     # apache2ctl -v && apache2 -v
      
  #     # - Instalação do Nginx
  #     sudo apt-get install -y nginx
  #     # nginx -v
      
  #     # - Instalação do PHP
  #     sudo wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
  #     sudo sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
  #     sudo apt-get install -y libapache2-mod-php php php-common php-xml php-gd php-opcache php-mbstring php-tokenizer php-json php-bcmath php-zip php-fpm -y
  #     # php -v
      
  #     # - Instalação do Composer
  #     sudo curl -sS https://getcomposer.org/installer | php
  #     sudo mv composer.phar /usr/local/bin/composer
  #     # composer --version
      
  #     ### Falta a configuração do Nginx para funcionar com PHP-FPM
  #     ##### LARAVEL
  #     # nano /etc/php/8.0/apache2/php.ini
  #     # # ---
  #     # cgi.fix_pathinfo=0 
  #     # date.timezone = America/Sao_Paulo
  #     # # ---
  #     # cd /var/www/html
  #     # composer create-project --prefer-dist laravel/laravel laravel
  #     # composer global require laravel/installer
  #     # chown -R www-data:www-data /var/www/html/laravel
  #     # chmod -R 775 /var/www/html/laravel
  #     # nano /etc/apache2/sites-available/laravel.conf
  #     # # ---
  #     # <VirtualHost *:80>
  #     #     ServerName laravel.example.com

  #     #     ServerAdmin admin@example.com
  #     #     DocumentRoot /var/www/html/laravel/public

  #     #     <Directory /var/www/html/laravel>
  #     #     Options Indexes MultiViews
  #     #     AllowOverride None
  #     #     Require all granted
  #     #     </Directory>

  #     #     ErrorLog ${APACHE_LOG_DIR}/error.log
  #     #     CustomLog ${APACHE_LOG_DIR}/access.log combined
  #     # </VirtualHost>
  #     # # ---
  #     # a2enmod rewrite
  #     # a2ensite laravel.conf
  #     # systemctl restart apache2
  #     # systemctl status apache2
  #   SHELL
  # end  
end
