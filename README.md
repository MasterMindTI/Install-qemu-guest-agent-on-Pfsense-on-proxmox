# Install-qemu-guest-agent-on-Pfsense-on-proxmox
## Instalação e ativação do qemu-guest-agent no pfSense 2.7.2 virtualizado no Proxmox 8.x

## Vamos para o Procedimento ?
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/bash/bash-original.svg" width="40" height="40"/> <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linux/linux-original.svg" width="40" height="40"/>
                
####################################################################
## 1. Pré-Requisitos
####################################################################
- 1.1. Servidor Proxmox 8.x
- 1.2. Pfsense 2.7.2 Virtualizado
- 1.3. Acesso a internet para download e instalação de pacotes
- 1.4. Acesso de root ao Firewall Pfsense

####################################################################
## 2. Instalação / Configuração
####################################################################

- 2.1. Instalação dos pacotes necessários

```
pkg install -y qemu-guest-agent
```

- 2.2. Adicionando variaveis dentro de "/etc/rc.conf.local"

```
cat > /etc/rc.conf.local << EOF
qemu_guest_agent_enable="YES"
qemu_guest_agent_flags="-d -v -l /var/log/qemu-ga.log"
#virtio_console_load="YES"
EOF
```

- 2.3. Configurando o arquivo "/usr/local/etc/rc.d/qemu-agent.sh" para subir o serviço do qemu-guest-agent

```
cat > /usr/local/etc/rc.d/qemu-agent.sh << EOF
#!/bin/sh
sleep 3
service qemu-guest-agent start
EOF
```

- 2.4. Setando a permissão de execução no arquivo "/usr/local/etc/rc.d/qemu-agent.sh"

```
chmod +x /usr/local/etc/rc.d/qemu-agent.sh
```

- 2.5. Subindo o serviço

```
service qemu-guest-agent start
```

*NOTA: Para homologar, reinicie a VM do Firewall Pfsense, e veja se o qemu-guest-agent, subiu automaticamente

####################################################################
## Informações Adicionais:
#### MasterMindTI - Instalação e configuração do qemu-guest-agent no pfSense 2.7.2 virtualizado no Proxmox
#### Procedimento: Install-qemu-guest-agent-on-Pfsense-on-proxmox
#### @Responsável: Miller Santos
#### @Data: 14/02/2024
#### @Versão: 1.0
#### @Homologado: Pfsense 2.7.2
####################################################################

### Qualquer dúvida, entre em contato.

e-mail: contato@mastermindti.com.br

## Contatos:

<div>
<a href="https://www.youtube.com/@mastermindti" target="_blank"><img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white" target="_blank"></a>
<a href = "mailto:contato@mastermindti.com.br"><img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white" target="_blank"></a>
<a href="https://www.linkedin.com/in/miller-guilherme-santos-42046471/" target="_blank"><img src="https://img.shields.io/badge/-LinkedIn-%230077B5?style=for-the-badge&logo=linkedin&logoColor=white" target="_blank"></a>   
</div>

## Estatisticas

<div>
<a href="https://github.com/MasterMindTI">
<img height="180em" src="https://github-readme-stats.vercel.app/api?username=MasterMindTI&show_icons=true&theme=dracula&include_all_commits=true&count_private=true"/>
</div>
