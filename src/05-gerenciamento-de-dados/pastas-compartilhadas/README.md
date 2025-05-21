# Compartilhamento de diretórios (pastas)

Para garantir a segurança e a privacidade dos dados, cada diretório de usuário no HPC Marvin possui permissão 700 ou `u:rwx, g:---, o:---`. Isso significa que apenas o próprio usuário "u" tem permissão de leitura "r", escrita "w" e execução "x", enquanto membros do grupo "g" e outros usuários "o" não têm acesso.

No entanto, em alguns casos, você pode precisar permitir o acesso a determinados diretórios, como para compartilhar um projeto com outros usuários. Abaixo, fornecemos um passo-a-passo básico de como você pode fazer isso.

## Passo-a-passo básico para dar permissão de acesso a outros usuários

1. Para compartilhar um diretório com outros usuários, você precisa começar alterarando as permissões do diretório `$HOME` para 711. Para isso, digite o comando `chmod 711 /home/<seu_nome_de_usuário>` no terminal.
2. Em seguida, utilize o comando `setfacl` para adicionar permissões de acesso a outros usuários. Por exemplo, para conceder permissão de leitura ao usuário "usuario1" no diretório "pasta_compartilhada", use o comando `setfacl -m u:usuario1:rx /caminho/da/pasta_compartilhada`._Obs: o `x` foi adicionado para que o usuário consiga executar o comando `ls`.
3. Para adicionar mais permissões, você pode usar outras opções como "w" para escrita e "x" para execução. Por exemplo, para dar ao usuário "usuario1" permissão de escrita e execução na pasta "pasta_compartilhada", use o comando `setfacl -m u:usuario1:rwx /caminho/da/pasta_compartilhada`.
4. Para verificar as permissões atuais do diretório, você pode usar o comando `getfacl` seguido do caminho do diretório. Por exemplo, para verificar as permissões atuais do diretório "pasta_compartilhada", você usaria o comando `getfacl /caminho/da/pasta_compartilhada`. Isso mostrará uma lista de usuários e suas respectivas permissões.
5. Se você quiser remover as permissões de acesso de um usuário específico, utilize o comando `setfacl -x` seguido do usuário desejado. Por exemplo, para remover as permissões de acesso do usuário "usuario1" no diretório "pasta_compartilhada", você usaria o comando `setfacl -x u:usuario1 /caminho/da/pasta_compartilhada`.
6. Para remover todas as permissões de acesso, você pode usar o comando `setfacl -b` seguido do caminho do diretório. Por exemplo, para remover todas as permissões de acesso no diretório "pasta_compartilhada", use comando `setfacl -b /caminho/da/pasta_compartilhada`.
7. Após remover as permissões, é recomendável verificar novamente as permissões com o comando `getfacl` para garantir que as permissões foram removidas corretamente.

## Criando links para pastas compartilhadas

A criação de um link para uma pasta compartilhada serve apenas para facilitar o acesso.

Vamos supor que o usuário `charles` compartilhou o acesso da pasta `projeto01` com `marie` seguindo os passos acima. Para que `marie` acesse a pasta compartilhada, ela pode criar um link simbólico para a pasta `projeto01` em seu diretório HOME. Para isso, ela pode usar o comando `ln -s /caminho/da/pasta_compartilhada /home/marie/projeto01`.

Obs: Links são como os atalhos no windows.

## Pastas compartilhadas e containers do singularity

Programas que estão instalados via singularity podem não ter acesso a pastas compartilhadas. Para resolver isso, você pode usar o comando `singularity run --bind /caminho/da/pasta/compartilhada:/caminho/dentro/do/container imagem.sif`.''

## Para melhor compreensão

Se você deseja aprimorar seus conhecimentos sobre o controle de acesso em sistemas Linux, aqui estão algumas fontes úteis:

- [An introduction to Linux Access Control Lists (ACLs)](https://www.redhat.com/sysadmin/linux-access-control-lists)
- [Red Hat Docs - Chapter25. Managing file permissions](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_basic_system_settings/assembly_managing-file-permissions_configuring-basic-system-settings)
- [Red Hat Docs - Chapter 28. Managing the Access Control List](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_basic_system_settings/assembly_managing-access-control-list_configuring-basic-system-settings)
- [Arch Linux Wiki - Access Control Lists (Português)](https://wiki.archlinux.org/title/Access_Control_Lists_(Portugu%C3%AAs))
- [Using ACLs](https://web.archive.org/web/20191220012518/http://vanemery.net:80/Linux/ACL/linux-acl.html)

Além disso, as páginas de manual (man pages) são excelentes recursos que estão disponíveis diretamente no terminal, basta digitar `man <nome_da_pagina>`. Você também pode acessá-las online. Aqui estão algumas man pages úteis relacionadas a listas de controle de acesso (_Access Control Lists - ACL_):

- chmod
- acl
- setfacl
- getfacl
