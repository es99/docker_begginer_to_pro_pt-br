# Blocos de construção do Linux

cgroups - limite de recursos
namespaces - isolamento de aplicação

## Cgroups
Recurso do kernel Linux que permite que processos sejam organizados em grupos hierárquicos cujo
o uso de vários tipos de recursos sejam limitados e monitorados.

Com cgroups, o _container runtime_ poderá especificar que um conteiner esteja apto para usar, por exemplo:
 - Até x% de ciclos de cpu (cpu.shares)
 - Até y% de memória (memory.limit_in_bytes)
 - Velocidade de leitura z MB/s (blkio.throttle.read_bps_device)

## Namespaces
Um namespace encapsula um recurso global do sistema em uma abstração que faz com que os processos dentro
do namespace acreditem que possuem sua própria instância isolada do recurso global.
 
As alterações no recurso global são visíveis para outros processos que são membros do mesmo namespace,
mas são invisíveis para outros processos que não são membros.

Com namespaces, um _conteiner runtime_ é capaz de manter processos fora do conteiner invisíveis dentro do
conteiner ou mapear usuário dentro do conteiner para um usuário diferente no host.

UTC namespace

unshare --uts
hostname demo
exit
hostname

IPC Namespace (Inter-Process Communication)
Process Namespace
 - Isola processos, faz com que um processo rodando numa conteiner não enxergue processos rodando em outro container, e também que os processos rodando em container não enxerguem os processos rodando na máquina host.


## Union filesystems
_Union filesystem_ permite que arquivos e diretórios de sistemas de arquivos separados, conhecidos como ramificações, sejam sobrepostos de forma transparente, formando um único sistema de arquivos coerente.
Os conteúdos de diretórios que possuem o mesmo caminho nas ramificações mescladas serão vistos juntos em um
único diretório mesclado, dentro do novo sistema de arquivos virtual.
Essa abordagem permite o uso eficiente de espaço porque camadas comuns podem ser compartilhadas. Por exemplo, se múltiplos conteineres da mesma imagem forem criados em um único _host_, o runtime do contêiner
só precisa alocar uma sobreposição fina _específica_ para cada conteiner, enquanto as camadas de imagem subjacentes podem ser compartilhadas. 

## Resumo
Docker consegue empacotar todas essas tecnologias que rodam no kernel linux e prover uma experiência de uso
conveniente ao usuário dentro de uma aplicação de desktop de fácil utilização.