# NIC.br Ansible

Este repositório guarda os arquivos para o laboratório de Ansible da palestra da NIC.br de 2022.

Para fazer o laboratório é preciso possuir um software de virtualização, conhecido como hypervisor, como por exemplo o [VirtualBox](https://www.virtualbox.org/). Para atender ao maior número de pessoas possíveis, todas as ferramentas utilizadas e recomendadas neste laboratório são livres e de código aberto.

Existem outros hypervisors como o [KVM](https://www.linux-kvm.org/page/Main_Page) para Linux ou outras soluções fechadas para Windows ou sistemas operacionais da Apple, porém o foco será sempre o VirtualBox.

Para criar o laboratório é possível utilizar o `Vagrant` ou baixar o arquivo [ansible.ova](https://drive.google.com/file/d/1uEnR26cJ0ybJswQS7Ll3R5553vNJVTMv/view?usp=sharing) e importá-lo no VirtualBox, a primeira forma é mais moderna e trás mais possibilidades de estudo para o usuário.

Escolha uma das opções abaixo para obter melhores instruções sobre como preparar o ambiente:

- [Vangrat](https://github.com/hector-vido/nicbr-ansible/tree/master/steps/vagrant.md)
- [ansible.ova](https://github.com/hector-vido/nicbr-ansible/tree/master/steps/ova.md)

**Atenção:**
- Será preciso habilitar a capacidade de virtualização do seu processador na "BIOS" do seu computador.
- O Vagrant tem maior compatibilidade com o `VirtualBox` e o `Libvirt`, nem todas as imagens estão disponíveis para todos os hypervisors.
- O funcionamento do `HyperV` com o Vagrant é parcial, as máquinas não conseguem ser configuradas com endereço IP fixo.
- O `HyperV` ou mesmo versões não originais do `VMWare Workstation` podem causar problemas nada óbvios no `VirtualBox`, não use software pirata, use Linux.
- Algums versões do Windows possuem componentes do `HyperV` instalados que podem causar problemas no `VirtualBox`.
- Até o momento não há hypervisors livres de arquitetura `amd64`(`x86_64`) para sistemas operacionais da Apple `arm64`, se possui uma máquina destas, venda, compre um computador de verdade e ajude alguém com o dinheiro que sobrar.
- O Fedora 36 está com problemas para configurar endereço IP fixo.

# Ansible

![Ansible](images/ansible.png)

Ansible é um projeto livre e de código aberto voltado para o provisionamento, gerência de configuração e implantação de software através de [Infraestrutura como Código](https://pt.wikipedia.org/wiki/Infraestrutura_como_C%C3%B3digo). Foi desenvolvido originalmente por Michael DeHaan e adquirido pela Red Hat em 2015.

De forma sucinta, as operações do Ansible acontecem através de uma máquina central, normalmente a mesma que está usando para ler este texto, se comunicando com outros dispositivos, APIs ou qualquer outro protocolo disponível.

Na grande maioria das vezes utilizamos o Ansible para se comunicar com outras máquinas, e apesar desta ser a sua principal função não é a sua única capacidada.

Diferente de outras ferramentas que trabalham com um servidor central e agentes, como [CFEngine](https://en.wikipedia.org/wiki/CFEngine) ou [Puppet](https://en.wikipedia.org/wiki/Puppet_(software)), o Ansible trabalha sozinho, e chamamos isso _"agentless"_ (sem agentes), afinal de contas, não devemos gerenciar o gerenciador não é mesmo?

Para fazer a conexões em outras máquinas o Ansible utiliza o bom e velho [**SSH**](https://pt.wikipedia.org/wiki/Secure_Shell) em máquinas Linux ou o [**winrm**](https://en.wikipedia.org/wiki/Windows_Remote_Management) em máquinas Windows, formas de conexão já conhecidas pelos profissionais de cada um destes sistemas.

## O Preço da Simplicidade

Apesar da arquitetura do Ansible ser bastante simples e convidativa, sua simplicidade trás uma desvantagem: gerenciar milhares de máquinas.

Enquanto outras soluções gerenciam as requisições dos agentes para evitar uma inundação de conexões ao mesmo tempo que podem deixar os agentes trabalhando por conta logo após entregar as instruções o Ansible precisa continuar conectado em cada máquina esperando o status de cada instrução.

Essa forma de trabalho torna-se um fardo para a máquina que executa o Ansible pois utiliza mais recursos do que outras soluções com agentes e dependendo da situação pode acabar levando muito mais tempo pois algumas das máquinas gerenciadas podem segurar a execução de algumas tarefas.

Isso não é o fim do mundo, primeiro porque ficará evidente somente com uma quantidade enorme de máquinas e segundo porque é possível contornar essa desvantagem utilizando outras [estratégias](https://docs.ansible.com/ansible/latest/user_guide/playbooks_strategies.html), paralelismo, dividir o trabalho entre diferentes máquinas controladores, etc.

## Conceitos Básicos

Existem um pouco mais de [conceitos básicos](https://docs.ansible.com/ansible/latest/network/getting_started/basic_concepts.html) oficias do Ansible, mas estes a seguir são suficientes para este laboratório.

### Nó de Controle

O nó de controle (*control node*) é a máquina que executa as ferramentas do ansible (`ansible`, `ansible-playbook`). Qualquer computador, ou coisa, que consiga instalar o Ansible e suas dependências pode ser utilizado - notebooks, máquinas virtuais, grandes servidores, containers.

### Nós Gerenciados

Os nós gerenciados (*managed nodes*), ou hosts, são os dispositivos alvo que pretendemos gerenciar com o Ansible, podem ser computadores, máquinas virtuais, dispositivos de rede, etc.

### Inventário

O inventário é uma lista de nós gerenciados, basicamente um arquivo de texto simples com informações pertinentes de cada nó. É muito comum utilizarmos o formato `.ini` já conhecido no Linux, mas podemos escrevê-los em outros formatos como `.json` ou `.yaml`.

### Playbooks

Playbooks são arquivos de texto fáceis de ler e escrever e descrevem as tarefas que queremos executar. As playbooks são escritas no formato de serialização [YAML](https://pt.wikipedia.org/wiki/YAML).

### Roles

As roles são como as playbooks mas são estruturadas de uma forma a facilitar sua reutilização, não se preocupe com as roles agora.

### Módulos

Os [módulos](https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html) são código ou binários que o Ansible transfere e executa em cada nó gerenciado. Todas as tarefas especificadas em uma playbook são baseadas em algum módulo.
