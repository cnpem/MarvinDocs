# Permissões de acesso

Por questões de segurança e privacidade dos dados, o diretório de cada usuário possui permissão 700 ou `u:rwx, g:---, o:---`. Isso significa que o próprio usuário "u" tem permissão de leitura "r", escrita "w" e execução "x", mas membros do grupo "g" e outros usuários "o", não tem nenhuma dessas permissões.

No entanto, em alguns cenários, você pode querer que outro usuário ou usuários, acessem alguma pasta específica. A pasta de um projeto por exemplo.

Abaixo descrevemos um passo-a-passo básico de como você pode fazer isso.

## Passo-a-passo básico

1. Para compartilhar uma pasta com outros usuários, primeiro você precisa mudar a permissão da pasta HOME para 711. Isso é feito digitando o comando `chmod 711 /home/<seu_nome_de_usuário>` na linha de comando.

2. Em seguida, você pode utilizar o comando "setfacl" para adicionar permissões de acesso a outros usuários. Por exemplo, para adicionar a permissão de leitura para o usuário "usuario1" na pasta "pasta_compartilhada", você usaria o comando `setfacl -m u:usuario1:r /caminho/da/pasta_compartilhada`.

3. Para adicionar mais permissões, você pode usar outras opções como "w" para escrita e "x" para execução. Por exemplo, para dar ao usuário "usuario1" permissão de escrita e execução na pasta "pasta_compartilhada", você usaria o comando `setfacl -m u:usuario1:rwx /caminho/da/pasta_compartilhada`.

4. Para verificar as permissões atuais da pasta, você pode usar o comando "getfacl" seguido do caminho da pasta. Por exemplo, para verificar as permissões atuais da pasta "pasta_compartilhada", você usaria o comando `getfacl /caminho/da/pasta_compartilhada`. Isso mostrará uma lista de usuários e suas respectivas permissões.

5. Se você quiser remover as permissões de acesso de um usuário específico, você pode usar o comando "setfacl -x" seguido do usuário desejado. Por exemplo, para remover as permissões de acesso do usuário "usuario1" na pasta "pasta_compartilhada", você usaria o comando `setfacl -x u:usuario1 /caminho/da/pasta_compartilhada`.

6. Para remover todas as permissões de acesso, você pode usar o comando "setfacl -b" seguido do caminho da pasta. Por exemplo, para remover todas as permissões de acesso na pasta "pasta_compartilhada", você usaria o comando `setfacl -b /caminho/da/pasta_compartilhada`.

7. Depois de remover as permissões, é recomendável verificar novamente as permissões com o comando "getfacl" para garantir que as permissões foram removidas corretamente.


## Para entender melhor

- [An introduction to Linux Access Control Lists (ACLs)](https://www.redhat.com/sysadmin/linux-access-control-lists)
- [Red Hat Docs - Chapter25. Managing file permissions](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_basic_system_settings/assembly_managing-file-permissions_configuring-basic-system-settings)
- [Red Hat Docs - Chapter 28. Managing the Access Control List](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_basic_system_settings/assembly_managing-access-control-list_configuring-basic-system-settings)
- [Arch Linux Wiki - Access Control Lists (Português)](https://wiki.archlinux.org/title/Access_Control_Lists_(Portugu%C3%AAs))
- [Using ACLs](https://web.archive.org/web/20191220012518/http://vanemery.net:80/Linux/ACL/linux-acl.html)

## man pages[^note]
- chmod
- acl
- setfacl
- getfacl

[^note]: man pages são páginas de documentação que estão acessíveis pelo próprio terminal atráves do comando `man <nome_da_pagina>`. Elas também podem ser acessadas online.

