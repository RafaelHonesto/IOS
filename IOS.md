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


**Funções da ACL**

```
¬ Limitam o tráfego e aumentam o desempenho da rede.

Ex: se a política corporativa não permite tráfego de vídeo na rede, as ACLs que
bloqueiam tráfego de vídeo podem ser configuradas e aplicadas.

Isso reduziria significativamente a carga da rede e aumentaria o desempenho da rede.

¬ Fornecer controle de fluxo de tráfego.

As ACLs podem restringir o fornecimento de atualizações de roteamento para garantir
que as atualizações sejam de uma fonte conhecida.

¬ Fornecer um nível básico de segurança para acesso à rede.
¬ Filtram tráfego com base no tipo de tráfego.
¬ Selecionam hosts para permitir ou negar acesso aos serviços de rede.

```
**Máscara Curinga**

```
ACL's utilizam a máscara curinga em suas configurações, elas são que os bits não utilizados das máscaras de rede normalmente usadas.

Exemplo:
Mascara de rede(MR) 255.255.255.0
Mascara Curinga(MC)  0.0.0.255

MR 255.255.254.0
MC 0.0.0.1.255

```
**Onde posicionar as ACL's?**

```
¬ Por exemplo, o tráfego que será negado em um destino remoto não deve ser
encaminhado usando recursos de rede na rota para esse destino.

Cada ACL deve ser posicionada onde há maior impacto sobre o aumento da
eficiência. As regras são:

* ACLs estendidas - Localize as ACLs estendidas o mais perto
possível da origem de tráfego a ser filtrado.

* Dessa forma, o tráfego não desejado é negado perto da rede de origem sem atravessar a
infraestrutura de rede.

* ACLs padrão - Como as ACLs padrão não especificam endereços de
destino, coloque-as o mais perto possível do destino.

Colocar uma ACL padrão na origem do tráfego impedirá, com eficiência, que o tráfego
acesse todas as outras redes através da interface onde é aplicada a ACL.

```


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
(config)# interface 
(config-if)# ip access-group [ID da ACL] [modo da ACL]

Modo da ACL 
pode ser in ou out
```
**Remover ACL da interface**
```
(config)#interface serial 0/0/0
(config-if)#no ip access-group [ID] [Modo]
```
**Criar ACL Numerica**
```
(config)#access-list access-list-number [ deny | permit | remark ] fonte [ source-wildcard ][ log ]

(config)#access-list [ID da ACL] permit/deny [Protocolo IP] [IP da rede origem] [Mascara curinga da rede] [Range da porta de origem] [IP de destino] [portas destino]


Exemplo:
Router(config)# access-list 20 permit 192.168.0.0 0.0.0.255
(config)#access-list 100 permit tcp 192.168.0.0 0.0.0.255 range 1024 65535 host 172.16.30.2 eq www



```

**Ver lista de ACL**

```
#show access-lists 

Standard IP access list 11
    10 deny 192.168.10.0 0.0.0.255 (8 match(es))
    20 permit any (7 match(es))
    
Deny: nega o acesso seguindo as configurações.
Permit: permite o acesso seguindo as configurações.

No exemplo acima, o router está negando o acesso da rede 192.168.10.0 e permitindo o acesso de qualquer outro IP.
    
```

**Criar e nomear ACL numerica**
```

(config)#access-list [ID da ACL] remark [Nome da ACL]

Exemplo:
(config)#access-list 1 remark Rede_LAN_S1

```
**Criar ACL Padrão nomeada**
```
(config)#ip acess-list standard [Nome da ACL]

Exemplo:
(config)#ip access-list standard NO_ACCESS
```

**Proteção Login com ACL**
```
line vty 0 4
login local
transport input ssh
access-class 21 in

```

** Criar ACL Extendida Nomeada (Consigo filtrar protocolos de Transporte (TCP e UDP)**
```

(config)# ip access-list extended [Nome da ACL]

```
## NAT 

**Verificar outside e inside em alguma interface**
```
#show run
```
**Verificar rotas**
```
#show ip nat statistics
```
**Ver Traduções**
```
#show ip nat translations
Pro  Inside global     Inside local       Outside local      Outside global
---  64.100.50.1       172.16.16.1        ---                ---
```
**Exemplo show run NAT**
```
#show run
interface GigabitEthernet0/0
 ip address 172.16.16.14 255.255.255.240
 ip nat inside
 duplex auto
 speed auto
!
interface Serial0/0/0
 ip address 209.165.128.130 255.255.255.248
 ip nat outside
!
```

**Ver tipos de NAT ativos**
```
#show ip nat statistics
Total translations: 1 (1 static, 0 dynamic, 0 extended)
Outside Interfaces: Serial0/0/0
Inside Interfaces: GigabitEthernet0/0
```

**Criar NAT Dinâmico**

Passo 1 - ACL
```
ip access-list standard [Nome da ACL]
permit [IP]
```
Passo 2 - Criar NAT Pool 
```
ip nat pool [Nome da NAT Pool] [ip inicial] [ip final] [mascara da rede]  
(exemplo: ip nat pool NAT_LAN 192.168.0.1 192.168.0.15 255.255.255.0)
```

Passo 3 - Criação NAT Dinamico
```
ip nat inside source list LAN pool Intervalo-IPs-WAN

```

**Criar PAT**

Um ip global interno para todos os ips internos, o que mudará será a porta por onde irá sair a conexão.


Passo 1 - Criar Pool com Unico Endereço
```
(config)#ip nat pool [Nome da Pool] [Primeiro IP] [Ultimo IP]
```
Passo 2 - Criar ACL
```
(config)#ip access-list standard [Nome da ACL]
Exemplo:
ip access-list standard PAT
permit 192.168.1.0 0.0.0.255
```

Passo 3 - Criar regra PAT aplicando na Interface
```
(config)#ip nat inside source list [Nome da ACL] [interface] orverload
```
Passo 3a - Criar regra PAT com pool
```
(config)#ip nat inside source list [Nome da ACL] pool [Nome da Pool]  orverload
```
NAT estatico e dinamico

Utiliza um ip global interno para cada ip local interno, 1 pra 1.

**Criar NAT Estatico (static) usando todas as porta**
```
(config)# ip nat inside/outside source static [IP local interno] [IP global interno]
ip nat inside source static 192.168.2.100 200.0.0.100
```

**Criar NAT Estatico (static) usando portas especificas**
```
(config)# ip nat inside/outside source static [IP local interno] [Porta] [IP global interno]
ip nat inside source static 192.168.2.100 80 200.0.0.3 8080
```

**Limpar tabela de NAT**
```
#clear ip nat translation *
STATIC sempre esta lá fixo
```
