
Formatar Pen Drive no Terminal Linux
===============================================

#### Sistemas de Arquivos ou File System, refere-se à forma como os dados são armazenados, organizados e acessados no disco pelo sistema operacional. É um artifício imposto pelo sistema operacional e não pelo hardware da máquina. O processo conhecido como "formatação lógica de disco" estabelece um file system em uma partição de HD, em pen drives, disquetes e etc.

----------

## Identificando o Pen Drive
1. Primeira Forma - Digite:
	
	> sudo fdisk -l

	- Exemplo de saída:

		Disco /dev/sda: 500.1 GB, 500107862016 bytes
		255 cabeças, 63 setores/trilhas, 60801 cilindros, total de 976773168 setores
		Unidades = setores de 1 * 512 = 512 bytes
		Tamanho do setor (lógico/físico): 512 bytes / 512 bytes
		Tamanho da E/S (mínimo/ideal): 512 bytes / 512 bytes
		Identificador do disco: 0x00000000
		
		Dispositivo Boot  | Início | Fim             | Blocos            | Id | Sistema
		---------------------|--------|---------------|-----------------|----|------------
		/dev/sda1	        | 1        | 976773167 | 488386583+ | ee | GPT

		Disco /dev/sdb: 4004 MB, 4004511744 bytes
		255 cabeças, 63 setores/trilhas, 486 cilindros, total de 7821312 setores
		Unidades = setores de 1 * 512 = 512 bytes
		Tamanho do setor (lógico/físico): 512 bytes / 512 bytes
		Tamanho da E/S (mínimo/ideal): 512 bytes / 512 bytes
		Identificador do disco: 0x36c439e6

		Dispositivo Boot | Início | Fim         | Blocos     | Id | Sistema
		--------------------|--------|------------|------------|----|------------------------
		/dev/sdb1           | 32      | 7821311 | 3910640 | 7  | HPFS/NTFS/exFAT
		

2. Segunda Forma - Digite:
	
	> mount

	- Exemplo de saída:

		/dev/sda2 on / type ext4 (rw,errors=remount-ro)
		proc on /proc type proc (rw,noexec,nosuid,nodev)
		sysfs on /sys type sysfs (rw,noexec,nosuid,nodev)
		none on /sys/fs/cgroup type tmpfs (rw)
		none on /sys/fs/fuse/connections type fusectl (rw)
		none on /sys/kernel/debug type debugfs (rw)
		none on /sys/kernel/security type securityfs (rw)
		none on /sys/firmware/efi/efivars type efivarfs (rw)
		udev on /dev type devtmpfs (rw,mode=0755)
		devpts on /dev/pts type devpts (rw,noexec,nosuid,gid=5,mode=0620)
		tmpfs on /run type tmpfs (rw,noexec,nosuid,size=10%,mode=0755)
		none on /run/lock type tmpfs (rw,noexec,nosuid,nodev,size=5242880)
		none on /run/shm type tmpfs (rw,nosuid,nodev)
		none on /run/user type tmpfs (rw,noexec,nosuid,nodev,size=104857600,mode=0755)
		none on /sys/fs/pstore type pstore (rw)
		/dev/sda1 on /boot/efi type vfat (rw)
		systemd on /sys/fs/cgroup/systemd type cgroup (rw,noexec,nosuid,nodev,none,name=systemd)
		gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,user=sim)
		/dev/sdb1 on /media/usuario/*PENDRIVE* type fuseblk(rw,nosuid,nodev,allow_other,default_permissions,blksize=4096) 

3. Terceira Forma - Digite:

	> lsblk

- Exemplo de saída:

		NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
		sda      8:0    0 465,8G  0 disk 
		├─sda1   8:1    0   512M  0 part /boot/efi
		├─sda2   8:2    0 461,8G  0 part /
		└─sda3   8:3    0   3,5G  0 part [SWAP]
		sdb      8:16   1   3,7G  0 disk 
		└─sdb1   8:17   1   3,7G  0 part /media/usuario/*PENDRIVE*
		sr0     11:0    1  1024M  0 rom 


--------------------

## Desmontar a unidade do Pen Drive

1. Normalmente, quando colocamos o Pen Drive na porta USB, o Linux (ou qualquer outros SO) já monta ele automaticamente, então para fazermos a formatação, devemos desmontá-lo. Digite o comando a baixo:

	> sudo umount CAMINHO/DA/UNIDADE

- Exemplo:
> sudo umount /dev/sdb1
***ou***
> sudo umount /media/usuario/PENDRIVE

--------------------

## Agora a formatação

1. Podemos formatá-lo para diversos formatos de Sistemas de Arquivos (mkfs.vfat, mkfs.ntfs, mkfs.bfs, mkfs.ext2, mkfs.ext3, mkfs.ext4, mkfs.minix, mkfs.msdos, mkfs.vfat, mkfs.xfs, mkfs.xiafs), mas irei demonstrar somente os 2 mais utilizados. Apesar de ser um dos mais primitivos programas de particionamento ainda em uso, o fdisk é o default nestes sistemas e por isso ainda muito usado.

	- Formato NTFS (recomentado):

		> sudo mkfs.ntfs -I /dev/sdb1
		***ou***
			sudo mkfs.ntfs -f -I /dev/sdb1
		**ou**	
			sudo mkntfs -I /dev/sdb1
		***ou***
			sudo mkntfs -f -I /dev/sdb1

		- Na formatação para NTFS, a maneira de nomear o dispositivo é diferente. Digite o seguinte comando:

			> sudo ntfslabel /dev/sdb1 NOMEPENDRIVE


	- Formato FAT32:

		> sudo mkfs.vfat -n NOMEPENDRIVE -I /dev/sdb1

--------------------

## Lista de comandos utilizados

**fdisk -l 	=>** Lista os particionamentos. fdisk é um utilitário presente em diversos sistemas operacionais que realiza particionamento de discos rígidos. Há versões do fdisk para Linux, DOS, Windows, FreeDOS e OS/2;

**mount =>** Comando para criar novos Sistemas de Arquivos e também para visualizar os já montados;

**lsblk =>** Exibe informações sobre as partições do HD e outros dispositivos de armazenamento como pen drives e CDs em formato de árvore;

**umount =>** Comando usado para desmontar Sistemas de Arquivos;

**mkfs =>** Comando responsável por formatar o sistema de aquivo;

**vfat =>** Formata no sistema de arquivos FAT32;

**ntfs =>** Formata no sistema de arquivos NTFS;

**-n =>** Nome que escolhido para o dispositivo;

**-I =>** Partição do Pen Drive (Não é obrigatório);

**-f =>** Executa a formatação rápida. Isso ignorará tanto a redução de volume quanto a verificação de setor ruim.

**ntfslabel =>** é uma ferramenta que possui a funcionalidade, renomear ou exibir o rótulo de um sistema de arquivos NTFS;

**/dev/sdb1 =>** Partição do disco onde é montado o dispositivo conectado. Sendo a primeira partição do segundo disco rígido SATA ou SCSI. Pode haver vários, por isso devemos ter certeza da partição que queremos formatar.

--------------------

## Breve explicação sobre os Sistemas de Arquivos NTFS e FAT32

- **NTFS (New Technology File System):** É um sistema de arquivos que surgiu juntamente com o lançamento do Windows NT. O NTFS possui várias características, em caso de falhas, por exemplo, quando o computador tem um desligamento repentino, ele tem a capacidade de reverter os dados para a condição anterior ao problema. Também possui a característica de suportar uma replicação de dados, como acontece nos sistemas RAID, por exemplo. O esquema de permissões de acesso é outra característica do NTFS. O NTFS dá a possibilidade de o usuário definir quem pode e como acessar pastas ou arquivos. Ele também possui muita eficiência no trabalho com grandes arquivos e também unidades de discos bastante cheias.
	
	- Características:
		- Cria partições maiores que 32GB;
		- Tem capacidade de compactar arquivos e economizar espaço em disco;
		- Conta com melhor gestão de espaço, assim, gerando menos fragmentação;
		- Possui menos espaço desperdiçado;
		- Conta com on-the-fly a criptografia de arquivos usando o EFS (Encrypting File System, o Windows Professional);
		- Tamanho máximo de volume: 2 32 clusters minus 1 cluster;
		- Tamanho máximo de arquivos: 2 44 bytes (16 TeraBytes) minus 64KB;
		- Número máximo de Clusters: 2 32 clusters minus 1 cluster.


- **FAT32 (File Allocation Table):** O sistema de arquivos FAT32 utiliza 32 bits no endereçamento de dados. Com o FAT32, é possível usar clusters menores, no geral de 4 KB, mesmo que a unidade ofereça maior capacidade de armazenamento. Assim, o desperdício acaba sendo menor.
	O sucesso da grande compatibilidade do FAT32 com programas, drivers de dispositivo e as redes existentes, foi reestruturado com o mínimo de alterações na arquitetura do Windows, nas estruturas de dados internos, em APIs e também no formato no disco. Como o FAT32 precisa de 4 bytes para poder armazenar valores do cluster, várias estruturas de dados internos e no disco e APIs publicados foram refeitas ou mesmo expandidas. Ferramentas e drivers existentes continuarão funcionando em unidades FAT32.
	Seguramente podemos dizer que o FAT32 é mais confiável. Ele tem a capacidade de posicionar o diretório principal em qualquer lugar do disco. Comparando com os sistemas antigos de FAT, havia uma grande limitação no número de entradas que podiam ser alocadas no diretório principal. Com o FAT32 não há essa preocupação. O FAT32 tem a capacidade de suportar partições de até 2 TB.
	
	- Características:
		- É compatível com todos os sistemas operacionais;
		- Ocupa menos espaço no disco USB;
		- Trabalha de forma mais rápida e com menos uso de memória;
		- Tamanho máximo de volume: 32GB for all OS. 2TB for some OS;
		- Tamanho máximo de arquivos: 4GB minus 2 Bytes;
		- Número máximo de Clusters: 4177918.

--------------------

## Fontes

http://www.guiafoca.org/cgs/guia/iniciante/ch-disc.html
	
http://pajeonline.blogspot.com.br/2011/07/como-formatar-em-ntfs-no-linux-hd.html

http://www.linuxdescomplicado.com.br/2013/12/voce-pergunta-como-formatar-um-pendrive.html

https://linux.die.net/man/8/mkntfs

http://www.techtudo.com.br/dicas-e-tutoriais/noticia/2011/12/como-formatar-um-pen-drive-no-terminal-do-linux.html

https://www.youtube.com/watch?v=6IuM2RHX6UQ

https://www.youtube.com/watch?v=Bq9whTuZ64Q

https://elias.praciano.com/2016/01/como-usar-o-comando-mount-para-visualizar-montar-e-desmontar-sistemas-de-arquivos-no-linux/

http://www.uniriotec.br/~morganna/guia/umount.html

http://www.uniriotec.br/~morganna/guia/lsblk.html

http://fdtk.com.br/wiki/tiki-index.php?page=ntfslabel