# NIC.br Ansible - ansible.ova

Baixe o arquivo [ansible.ova](https://drive.google.com/file/d/1orTDlmB6Hn9jfBi7LTJNgsZ-YIkmiwyz) em seu computador.

Um arquivo `.ova` é um pacote com definições e discos de máquinas virtuais. Neste nosso caso haverão quatro máquinas dentro deste arquivo.

É possível abrir arquivos `.ova` em vários hypervisors, convertê-los ou extraí-los para utilizar em outros mais, mas neste nosso caso o foco será única e exclusivamente o VirtualBox.

Três passos serão necessários para conseguirmos acesso as máquinas:

- Baixar o arquivo
- Importar o arquivo dentro do VirtualBox
- Criar uma interface de rede para `192.168.56.0/24`

### Importando o arquivo .ova

### Adicionando a interface de rede

Muitas vezes esta interface de rede já existe por padrão dentro do VirtualBox.
