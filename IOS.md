# Comandos Cisco IOS

Esse são os comandos utilizados em sala de aula, USE como consulta caso esteja em dúvida em alguma configuração.

## Configurações Iniciais (Switch e Router)

**Entrar no modo Exec Privilegiado**
```
>enable
```

**Mostrar as configurações que estão ativas no equipamentos**
```
#show running-config
```

**Mostrar as configurações que estão salvas no equipamentos**
```
#show startup-config
```

**Salvas as configurações que estão do equipamentos**
```
#copy running-config startup-config
ou
#write memory
ou
#wr
```

**Reiniciar o equipamento**
```
#reload
```

**Apagar todas as configurações salvas**
```
#write erase
```

**Destravar o terminal**
```
Ctrl+Shift+6
```

**Ir para a tela de configuração do equipamento**
```
#configure terminal
```

**Mudar nome do equipamentos**
```
(config)#hostname [nome]
```

**Inserir um banner de entrada**
```
(config)#banner motd "[mensagem]"
```

**Inserir senha de Enable**
```
(config)#enable secret [senha] (Criptografada)

(config)#enable password [senha] (Sem criptografia)
```

**Inserir senha na console**
```
(config)#line console [número-da-console]
(config-line)#password [senha]
(config-line)#login
```

**Encriptar todas as senhas que estão em texto plano**
```
(config)#service password-encryption
```

**Anular qualquer commando no CISCO IOS**
```
'no' na frente do comando
Exemplo: no hostname SW-01 --> (Apagar o nome configurado no Switch)
```

**Voltar para a tela de EXEC-Privilegiado**
```
Atalho no Teclado: Ctrl+Z
ou
Comando: end
```

**Mostrar a tabela MAC do Switch**
```
#show mac-address-table (IOS 12.2)

#show mac address-table dynamic (IOS 15.0)
```

**Ver arquivos na memória Flash**
```
#dir flash
```

**Ver arquivos na memória NVRAM**
```
#dir nvram
```

**Desativar a paginação (--MORE--)**
```
#terminal length 0
```
**Desativar as mensagens de erro na tela**
```
(config)#no logging console
```

**Configurar várias Interfaces ao mesmo tempo**

**Exemplo**: Configurar todas as interfaces entre a f0/1 e a f0/5
```
(config)#interface range f0/1-5
```

**Mostrar resumo das interfaces do Equipamento**
```
#show ip interface brief
```

**Inserir uma descrição em uma Interface**
```
(config-if)#description [texto-da-descrição]
```

**Desativar uma interface**
```
(config-if)#shutdown
```

**Ativar uma Interface**
```
(config-if)#no shutdown
```

**Definir nome do domínio no dispositivo**
```
(config)#ip domain-name [nome-do-domínio]
```

**Gerar chave de criptografia**
```
(config)#crypto key generate rsa general-key modulus [tamanho-da-chave-em-bits]
```

**Criar usuário local**
```
(config)#username [nome-do-usuário] privilege [nível-de-privilégio] secret [senha-do-usuário]
```

**Configurar acesso via SSH em todas as linhas VTY**
```
(config)line vty 0 15
(config-line)transport input ssh
```

**Ativar o login com usuário e senha local (funciona para as linhas de Console e VTY)**
```
(config-line)#login local
```

**Desativar tradução de nome**
```
(config)#no ip domain-lookup
```

## Configurações do Switch

**Configurar endereço IP em um Switch**
```
(config)#interface vlan [id-da-vlan-de-gerenciamento]
(config-if)#ip address [endereço-ip] [máscara (em decimal)]
(config-if)#no shutdown

Lembrando que você deve criar a VLAN de Gerenciamento, do contrário o Switch não vai ativar o endereço IP
```

**Configurar o Gateway Padrão no Switch**
```
(config)#ip default-gateway [ip-do-gateway]
```

## Configurações do Roteador

**Configurar IP em uma Interface ou Subinterface**
```
(config-if)#ip address [endereço-ip] [máscara (em decimal)]
```

**Exibir a tabela de roteamento**
```
#show ip route
```

**Criação de Subinterface e atrelamento dela a uma VLAN**

Para configurar uma Subinterface, basta colocar um **ponto** no final do nome da Interface onde você quer criar a **Subinterface**, após o ponto digite o **ID da Subinterface**, lembrando que o **ID da Subinterface** normalmente é o **ID da VLAN** a qual essa Subinterface será atrelada.

No exemplo abaixo vamos criar a **Subinterface .10** na **Interface g0/0** e atrelar ela a **VLAN 10**

```
(config)#interface g0/0.10
(config-if)#encapsulation dot1q 10
```

**Definir um tamanho mínimo de senha para os usuários locais**
```
(config)#security password min-length [tamanho-mínimo]
```

**Bloquear acesso de um usuário, após muitas tentativas de acesso**
```
Exemplo: Bloquear um usuário por 30 Segundos, caso ele erre a senha 3 vezes, em um período de 60 segundos

(config)#login block-for 30 attempts 3 within 60 
```

**Criar Rota Estática**
```
(config)#ip route [rede-de-destino] [máscara-da-rede-de-destino] [interface-de-saída]

ou

(config)#ip route [rede-de-destino] [máscara-da-rede-de-destino] [ip-do-roteador-que-conhece-a-rede]
```

**Configurar Rota Padrão**
```
(config)#ip route 0.0.0.0 0.0.0.0 [ip-de-último-recurso]
```

## Configurações IPv6

**Ver resumo dos endereços IPv6 configurados no equipamento**
```
#show ipv6 interface brief
```

**Habilitar Roteamento IPv6**
```
(config)#ipv6 unicast-routing
```

**Configurar IPv6 em uma Interface ou Subinterface**
```
(config-if)#ipv6 address [endereço-ip]/[prefixo]
```

**Configurar IPv6 Link Local em uma Interface ou Subinterface**
```
(config-if)#ipv6 address [endereço-ip]/[prefixo] link-local
```

**Configurar Rota Estática IPv6**
```
(config)#ipv6 route [rede-de-destino]/[prefixo] [ip-do-roteador-que-conhece-a-rede]

ou

(config)#ipv6 route [rede-de-destino]/[prefixo] [interface-de-saída]
```

**Configurar Rota Padrão IPv6**
```
(config)#ipv6 route ::/0 [ip-de-último-recurso]
```

## Configurações de VLAN

**Criar e definir um nome para uma VLAN**
```
(config)#vlan [id-da-vlan]
(config-vlan)#name [nome-da-vlan]
```

**Atrelar uma VLAN a uma interface**
```
(config)#interface [id-da-interface]
(config-if)#switchport mode access
(config-if)#switchport access vlan [id-da-vlan]
```

**Configurar o Trunk em uma interface**
```
(config)#interface [id-da-interface]
(config-if)#switchport mode trunk
(config-if)#switchport trunk native vlan [id-da-vlan_nativa]
(config-if)#switchport trunk allowed vlan [id-das-vlans (separado por vírgula)]
```

**Exibir um resumo das VLANs presentes no dispositivo e as interfaces atreladas as VLANs**
```
#show vlan brief
```

**Exibir informações sobre uma VLAN específica**
```
#show vlan id [id-da-vlan]
ou
#show vlan name [nome-da-vlan]
```

**Exibir informações relacionadas a VLAN em um interface específica**
```
#show interface [id-da-interface] switchport
```

**Deletar arquivo vlan.dat**
```
#delete vlan.dat
```

## Spanning Tree 

**Aqui identificamos se o switch é root bridge da VLAN**
```
#show spanning-tree vlan [id-da-vlan]
```

**Filtro para buscar porta FastEthernet dentro das Interfaces**
```
# show interfaces | in FastEthernet 
```

**Ver todas as interfaces conectadas do Spanning-tree**
```
#show spanning-tree detail
 ```

**Ver MAC somente das interfaces conectadas e ativas**
```
#show mac-address-table
```

**Ver MAC somente das interfaces conectadas e não ativas**
```
# show interfaces | in line protocol | address
```
**Mudar o Switch (Root Bridge) - Verificar qual a prioridade do Root ID antes de mudar**
```
(config)#spanning-tree vlan [id-da-vlan] priority 28672
```

**Mudar o Switch RootBrigde**
```
(config)#spanning-tree vlan [id's-da-vlan] root primary
```

## Etherchannel

**Visualizar Portas**
```
#show ip int brief
```

**Visualizar Canal Etherchannel**
```
#show etherchannel summary
```
**Visualizar Canal Etherchannel por Porta**
```
#show etherchannel 
```

**Mostram o port channel como um link lógico.**
```
#show interfaces trunk 
#show spanning-tree 
```


**Configurar Link Aggreggation LACP**
```
(config)# interface range gigabitEthernet 1/1-2
(config-if)# channel-protocol lacp
(config-if)# channel-group 1 mode active
ou
(config-if)# channel-group 1 mode passive
```

**Configurar Link Aggreggation PAgP**
```
(config)# interface range gigabitEthernet 1/1-2
```
```
(config-if)# channel-protocol pagp
```
```
(config-if)# channel-group 1 mode auto
ou
(config-if)# channel-group 1 mode desirable
```
**Status das Portas**
```
#show port-channel summary

Sinalizadores: 
D - Down (desligado)
P - port-channel está Up (ligado) (membros estão funcionais)
I - Individual 
H - Hot-standby (Link em espera) (somente LACP)
s - recurso suspenso - módulo removido
S - Comutado 
R - Roteado
U – Up (ligado) (canal lógico)

interface GigabitEthernet1/1
 channel-protocol lacp
 channel-group 1 mode active
!
interface GigabitEthernet1/2
 channel-protocol lacp
 channel-group 1 mode active
!
interface Port-channel 1
```
Observar que foi criada uma interfadce virtual chamada Port-channel 1
Toda mudança é feita na porta "Port-channel 1"


## Access Control List (ACL)

**Verificar as ACLs**
```
#show access-lists
```
**Verificar em qual porta esta aplicada a ACL**
```
show running-config
```

**Atrelar ACL a interface**
```
interface serial 0/0/0
ip access-group 11 out
```
**Remover ACL da interface**
```
interface serial 0/0/0
no ip access-group 11 out
```
**Criar ACL Numerica**
```
access-list 100 permit tcp 192.168.0.0 0.0.0.255 range 1024 65535 host 172.16.30.2 eq www
show access-lists 

Standard IP access list 11
    10 deny 192.168.10.0 0.0.0.255 (8 match(es))
    20 permit any (7 match(es))
```

**Criar e nomear ACL numerica**
```
(config)#access-list 1 remark Rede_LAN_S1
(config)#access-list 1 permit 192.168.10.0 0.0.0.255
(config)#access-list 1 deny any
(config)#do show access-list
```
**Criar ACL Padrão nomeada**
```
ip access-list standard NO_ACCESS
(config-std-nacl)#20 permit any
(config-std-nacl)#10 deny host 192.168.11.10
```

**Proteção Login com ACL**
```
line vty 0 4
login local
transport input ssh
access-class 21 in
exit
access-list 21 permit 192.168.10.0 0.0.0.255
access-list 21 deny any
```
