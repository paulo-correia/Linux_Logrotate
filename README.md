# Logrotate

A ferramenta logrotate tem como objetivo rotacionar automaticamente logs de aplicativos segundo a necessidade e a organização que o administrador de sistemas (SysAdmin) deseje.

Todo administrador experiente reconhece a importância dos logs e principalmente o quão relevante é ter os logs disponíveis e organizados para um momento onde é necessária uma rápida consulta aos mesmos.

Esta ferramenta é muito útil para os SysAdmin e possui recursos flexíveis que por vezes não são explorados.

É relevante salientar que alguns aplicativos possuem seu desempenho comprometido quando seus arquivos de log chegam a tamanhos muito grandes.

## Instalação

Toda a instalação é feita como root

### Debian

Instale o pacote do logrotate com o comando:

`apt-get install logrotate`

### CentOS

 Instale o pacote do logrotate com o comando:

`yum -y install logrotate`

## Configuração

`/etc/logrotate.conf`

daily - diariamente

weekly - semanalmente

montly - mensalmente

yearly - anualmente

rotate x - quantas rotações (52 arquivos no exemplo abaixo)

Exemplo usando o log do apache:

 ```
/var/log/apache2/*.log {
        weekly
        missingok
        rotate 52
        compress
        delaycompress
        notifempty
        create 640 root adm
        sharedscripts
        postrotate
                /etc/init.d/apache2 reload > /dev/null
        endscript
 }
```

### Colocando um log para rotacionar

Crie um arquivo em /etc/logrotate.d

(Preferencialmente o nome do arquivo seja o nome do log)

Caso queira copie um dos arquivos existentes para o arquivo que deseja criar e edite-o

Exemplo:

 ```
 /caminho/para/o/log/arquivo.log {
       tipo_de_rotacao
       compress
       rotate 3
       create 600 root root       
}
```

Onde:

tipo\_de\_rotacao - (daily, weekly, montly, yearly, size \[tamanho\])

compress - comprime o arquivo

create \[permissão\] \[usuário\] \[grupo\] - Ao criar um arquivo novo aplica a permissão, e cria com o usuário e grupo

rotate \[quantidade\] - Cria até a quantidade de arquivos, depois sobreescreve