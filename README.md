# NIC.br Ansible

Este repositório guarda os arquivos para o laboratório de Ansible da palestra da NIC.br de 2022.

Para fazer o laboratório é preciso possuir um software de virtualização, conhecido como hypervisor, como por exemplo o [VirtualBox](https://www.virtualbox.org/). Para atender ao maior número de pessoas possíveis, todas as ferramentas utilizadas e recomendadas neste laboratório são livres e de código aberto.

Existem outros hypervisors como o [KVM](https://www.linux-kvm.org/page/Main_Page) para Linux ou outras soluções fechadas para Windows ou sistemas operacionais da Apple, porém o foco será sempre o VirtualBox.

Para criar o laboratório é possível utilizar o `Vagrant` ou baixar o arquivo [ansible.ova](https://drive.google.com/file/d/1orTDlmB6Hn9jfBi7LTJNgsZ-YIkmiwyz) e importá-lo no VirtualBox, a primeira forma é mais moderna e trás mais possibilidades de estudo para o usuário.

Escolha uma das opções abaixo para obter melhores instruções sobre como preparar o ambiente:

- [Vangrat](https://github.com/hector-vido/nicbr-ansible/tree/master/instrucoes/vagrant.md)
- [ansible.ova](https://github.com/hector-vido/nicbr-ansible/tree/master/instrucoes/ova.md)

**Atenção:**
- Será preciso habilitar a capacidade de virtualização do seu processador na "BIOS" do seu computador.
- O Vagrant tem maior compatibilidade com o `VirtualBox` e o `Libvirt`, nem todas as imagens estão disponíveis para todos os hypervisors.
- O funcionamento do `HyperV` com o Vagrant é parcial, as máquinas não conseguem ser configuradas com endereço IP fixo.
- O `HyperV` ou mesmo versões não originais do `VMWare Workstation` podem causar problemas nada óbvios no `VirtualBox`, não use software pirata, use Linux.
- Algums versões do Windows possuem componentes do `HyperV` instalados que podem causar problemas no `VirtualBox`.
- Até o momento não há hypervisors livres de arquitetura `amd64`(`x86_64`) para sistemas operacionais da Apple `arm64`, se possui uma máquina destas, venda, compre um computador de verdade e ajude alguém com o dinheiro que sobrar.

# Ansible
