# NIC.br Ansible

Este repositório guarda os arquivos para o laboratório de Ansible da palestra da NIC.br de 2022.

Para fazer o laboratório é preciso possuir um software de virtualização, conhecido como hypervisor, como por exemplo o [VirtualBox](https://www.virtualbox.org/). Para atender ao maior número de pessoas possíveis, todas as ferramentas utilizadas e recomendadas neste laboratório são livres e de código aberto.

Existem outros hypervisors como o [KVM](https://www.linux-kvm.org/page/Main_Page) para Linux ou outras soluções fechadas para Windows ou sistemas operacionais da Apple, porém o foco será sempre o VirtualBox.

Para criar o laboratório é possível utilizar o `Vagrant` ou baixar o arquivo `.ova` e importá-lo no VirtualBox, a primeira forma é mais moderna e trás mais possibilidades de estudo para o usuário.

## Vagrant

Vagrant é uma ferramenta que auxilia a criação de ambientes reproduzíveis, normalmente utilizando máquinas virtuais.

Através do Vagrant não precisamos nos preocupar em instalar e configurar nossas máquinas virtuais, e também não precisamos mais compartilhar pacotes imensos entre aqueles que desejam o mesmo ambiente, tudo o que precisamos é de apenas alguns arquivos e nosso `Vagrantfile`.

A flexibilidade do Vagrant se apoia em imagens de sistemas operacionais pré-configurados com a possibilidade de execução de comandos durante o provisionamento.

O Vagrant se comunica com o hypervisor e faz todas as operações necessárias para provisionar as máquinas virtuais e facilitar a gerência, por exemplo, configurando IP fixo e facilitando o acesso via `ssh`.

### Vagrantfile

O `Vagrantfile` é responsável pela criação e configuração do nosso ambiente, sendo capaz de reproduzir os mesmos passos quantas vezes for executado, sem a necessidade de intervenção manual. O trecho abaixo é um exemplo de um `Vagrantfile`  que configura uma máquina [Debian](https://www.debian.org/) com o servidor web [Apache](https://httpd.apache.org/).

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  config.vm.box = "debian/bullseye64"

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y apache2
  SHELL

end
```

### Utilização

Para utilizar o Vagrant primeiro é preciso instalá-lo, existem versões do Vagrant disponíveis nos mais variados repositórios das distribuições e também há uma versão isolada para os principais sistemas operacionais. As instruções de instalação estão em https://www.vagrantup.com/downloads.

O Vagrant se integra muito bem ao VirtualBox e ao Libvirt (que utiliza KVM) do Linux, mas o mesmo não ocorre para outros hypervisors, lembre-se disso caso queira utilizar um hypervisor diferente.

Uma vez que o Vagrant e o seu hypervisor estejam instalados, "clone" (com o git) este repositório ou baixe o arquivo [.zip](https://github.com/hector-vido/nicbr-ansible/archive/refs/heads/master.zip) com os arquivos necessários e os descompacte.

#### git clone

```bash
git clone https://github.com/hector-vido/nicbr-ansible
cd nicbr-ansible
```

#### .zip

Ao baixar e descompactar o arquivo .zip um diretório chamado `nicbr-ansible-master` será criado, acesse-o:

```bash
cd nicbr-ansible-master
```

Todos os comandos do Vagrant devem ser executados no mesmo diretório do arquivo `Vagrantfile`, alguns exemplos:

```bash
vagrant up # cria as máquinas
vagrant up fedora # cria apenas a máquina fedora
vagrant halt # desliga todas as máquinas
vagrant halt opensuse # desliga apenas a máquina opensuse
vagrant destroy # desliga e destroy todas as máquinas
vagrant ssh debian # acessa a máquina debian via SSH
```

Você deve executar `vagrant up` isso criará todas as máquinas. Na primeira vez que rodar esse comando as imagens de cada sistema serão baixadas e isso pode levar algum tempo, nas próximas vezes o processo será muito mais rápido pois as imagens estarão presentes na sua máquina.

## Ansible