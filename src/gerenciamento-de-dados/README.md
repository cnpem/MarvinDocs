# Gerenciamento de Dados

Este capítulo aborda as estratégias de gerenciamento de dados para o cluster HPC Marvin, incluindo as melhores práticas para armazenamento, transferência e backup de dados.

## Armazenamento de Dados 🗃️

O HPC Marvin fornece armazenamento em disco para os usuários. Este tópico apresenta informações sobre as opções de armazenamento disponíveis e as melhores práticas para gerenciamento de dados. Serão discutidos os seguintes tópicos:

- Opções de armazenamento: disco local e compartilhado.
- Montagem e desmontagem de sistemas de arquivos.
- Práticas recomendadas de gerenciamento de espaço em disco.
- Gerenciamento de permissões de acesso a arquivos.

## Transferência de Arquivos 📁🔄💻 

Para começar a utilizar o HPC Marvin, é necessário transferir seus arquivos para o sistema. Isso pode ser feito de várias maneiras, como usando o comando `scp` (secure copy)[^note1], o comando `rsync`[^note2] ou usando um cliente FTP (File Transfer Protocol). Para transferir seus arquivos, siga as instruções fornecidas abaixo:

1. Abra um terminal em seu computador
2. Use o comando `scp`, o comando `rsync`, ou um cliente FTP para transferir seus arquivos para o sistema

[^note1] [https://linux.die.net/man/1/scp](https://linux.die.net/man/1/scp)

[^note2] [https://linux.die.net/man/1/rsync](https://linux.die.net/man/1/rsync)

## Backup de Dados 💾

O backup de dados é essencial para garantir a integridade dos dados armazenados no HPC Marvin. Este tópico aborda as melhores práticas para backup de dados, incluindo:

- Opções de backup disponíveis.
- Como agendar backups regulares.
- Gerenciamento de restauração de dados.

Esperamos que este capítulo ajude você a gerenciar seus dados de forma eficiente e segura no HPC Marvin. Se você tiver alguma dúvida ou feedback sobre o conteúdo deste manual, não hesite em entrar em contato conosco.

## Permissões de Acesso 🔑

Para garantir a segurança e a privacidade dos dados, cada diretório de usuário no HPC Marvin possui permissão 700 ou `u:rwx, g:---, o:---`. Isso significa que apenas o próprio usuário "u" tem permissão de leitura "r", escrita "w" e execução "x", enquanto membros do grupo "g" e outros usuários "o" não têm acesso.

No entanto, em alguns casos, você pode precisar permitir o acesso a determinados diretórios, como para compartilhar um projeto com outros usuários. Abaixo, fornecemos um passo-a-passo básico de como você pode fazer isso.

### Passo-a-passo básico

1. Para compartilhar um diretório com outros usuários, você precisa alterar as permissões do diretório HOME para 711. Para isso, digite o comando `chmod 711 /home/<seu_nome_de_usuário>` no terminal.

2. Em seguida, utilize o comando `setfacl` para adicionar permissões de acesso a outros usuários. Por exemplo, para conceder permissão de leitura ao usuário "usuario1" no diretório "pasta_compartilhada", use o comando `setfacl -m u:usuario1:r /caminho/da/pasta_compartilhada`.

3. Para adicionar mais permissões, você pode usar outras opções como "w" para escrita e "x" para execução. Por exemplo, para dar ao usuário "usuario1" permissão de escrita e execução na pasta "pasta_compartilhada", use o comando `setfacl -m u:usuario1:rwx /caminho/da/pasta_compartilhada`.

4. Para verificar as permissões atuais do diretório, você pode usar o comando `getfacl` seguido do caminho do diretório. Por exemplo, para verificar as permissões atuais do diretório "pasta_compartilhada", você usaria o comando `getfacl /caminho/da/pasta_compartilhada`. Isso mostrará uma lista de usuários e suas respectivas permissões.

5. Se você quiser remover as permissões de acesso de um usuário específico, utilize o comando `setfacl -x` seguido do usuário desejado. Por exemplo, para remover as permissões de acesso do usuário "usuario1" no diretório "pasta_compartilhada", você usaria o comando `setfacl -x u:usuario1 /caminho/da/pasta_compartilhada`.

6. Para remover todas as permissões de acesso, você pode usar o comando `setfacl -b` seguido do caminho do diretório. Por exemplo, para remover todas as permissões de acesso no diretório "pasta_compartilhada", use comando `setfacl -b /caminho/da/pasta_compartilhada`.

7. Após remover as permissões, é recomendável verificar novamente as permissões com o comando `getfacl` para garantir que as permissões foram removidas corretamente.

### Para melhor compreensão

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

Completar essas etapas iniciais é essencial para garantir que você possa utilizar o HPC Marvin de forma eficiente. Se você tiver alguma dúvida ou precisar de ajuda, não hesite em entrar em contato com a equipe de suporte do sistema.
