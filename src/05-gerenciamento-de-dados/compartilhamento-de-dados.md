# Compartilhamento de dados

Os dados são compartilhados a nível de usuário no HPCC Marvin, usando o sistema de controle de acesso do Linux, conhecido como _Access Control Lists_ ([ACLs](https://www.redhat.com/sysadmin/linux-access-control-lists)). As ACLs permitem que você defina permissões específicas para usuários e grupos em diretórios e arquivos, facilitando o compartilhamento seguro de dados entre usuários.

Para garantir a segurança e a privacidade dos dados, cada diretório de usuário no HPCC Marvin possui permissão 700 ou `u:rwx, g:---, o:---`. Isso significa que apenas o próprio usuário "u" tem permissão de leitura "r", escrita `w` e execução `x`, enquanto membros do grupo `g` e outros usuários `o` não têm acesso.

No entanto, em alguns casos, você pode precisar permitir o acesso a determinados diretórios, como para compartilhar um projeto com outros usuários.

## Usando o ACL para compartilhar dados

Nesta seção, vamos usar o usuário hipotético `marie.curie` como exemplo para demonstrar como compartilhar dados com outros usuários no HPCC Marvin.

### Verificando as permissões

Para verificar as permissões de um arquivo ou um diretório específico, use o seguinte comando no terminal:

```bash
getafcl /caminho/do/diretorio_ou_arquivo
```

Por exemplo, para verificar as permissões do seu `HOME`, você pode usar:

```bash
$ getafcl /home/marie.curie
# file: /home/marie.curie
# owner: marie.curie
# group: domain\040users
user::rwx
group::---
other::---
```

### Concedendo permissão de acesso a outros usuários

Primeiramente, para compartilhar um arquivo ou diretório com outros usuários, você precisa começar alterarando as permissões do diretório `$HOME` para 711. Para isso, use o comando:

```bash
chmod 711 /home/marie.curie
```

Então, cheque as mudanças com o comando `getfacl`:

```bash
$ getfacl /home/marie.curie
# file: /home/marie.curie
# owner: marie.curie
# group: domain\040users
user::rwx
group::--x
other::--x
```

Em seguida, você pode usar o comando `setfacl` para adicionar permissões de acesso a outros usuários. Por exemplo, para conceder permissão de leitura ao usuário "joao.guerra" no diretório "pasta_compartilhada", use o comando:

```bash
setfacl -m u:joao.guerra:r-x /home/marie.curie/pasta_compartilhada
```

<div class="warning">
A opção <code>x</code> foi adicionado para que o usuário consiga executar o comando <code>ls</code> e listar os arquivos dentro do diretório compartilhado.
</div>

Então, cheque as mudanças com o comando `getfacl`:

```bash
$ getfacl /home/marie.curie/pasta_compartilhada
# file: /home/marie.curie/pasta_compartilhada
# owner: marie.curie
# group: domain\040users
user::rwx
user:joao.guerra:r-x
group::--x
mask::r-x
other::--x
```

Caso você queira dar permissões de acesso recursivamente para todos os arquivos e subdiretórios dentro de "pasta_compartilhada", você pode usar a opção `-R`:

```bash
setfacl -R -m u:joao.guerra:r-x /home/marie.curie/pasta_compartilhada
```

Caso você queira conceder acesso para todas os arquivos e subdiretórios que podem ser criados dentro de "pasta_compartilhada", você pode usar a opção `-d`:

```bash
setfacl -d -m u:joao.guerra:r-x /home/marie.curie/pasta_compartilhada
```

Então, cheque novamente as mudanças com o comando `getfacl`:

```bash
$ getfacl /home/marie.curie/pasta_compartilhada
# file: /home/marie.curie/pasta_compartilhada
# owner: marie.curie
# group: domain\040users
user::rwx
user:joao.guerra:r-x
group::--x
mask::r-x
other::--x
default:user::rwx
default:user:joao.guerra:r-x
default:group::--x
default:mask::r-x
default:other::--x
```

Para adicionar mais permissões, você pode usar outras opções como `w` para escrita e `x` para execução. Por exemplo, para dar ao usuário "joao.guerra" permissão de escrita e execução na pasta "pasta_compartilhada", use o comando:

```bash
setfacl -m u:joao.guerra:rwx /home/marie.curie/pasta_compartilhada
```

Então, cheque novamente as mudanças com o comando `getfacl`:

```bash
$ getfacl /home/marie.curie/pasta_compartilhada
# file: /home/marie.curie/pasta_compartilhada
# owner: marie.curie
# group: domain\040users
user::rwx
user:joao.guerra:rwx
group::--x
mask::rwx
other::--x
default:user::rwx
default:user:joao.guerra:r-x
default:group::--x
default:mask::r-x
default:other::--x
```

### Removendo permissões de acesso

Para remover as permissões de acesso de um usuário específico, utilize o comando `setfacl -x` seguido do usuário desejado. Por exemplo, para remover as permissões de acesso do usuário "joao.guerra" no diretório "pasta_compartilhada", use o comando:

```bash
setfacl -x u:joao.guerra /home/marie.curie/pasta_compartilhada
```

Então, cheque novamente as mudanças com o comando `getfacl`:

```bash
$ getfacl /home/marie.curie/pasta_compartilhada
# file: /home/marie.curie/pasta_compartilhada
# owner: marie.curie
# group: domain\040users
user::rwx
group::--x
other::--x
default:user::rwx
default:user:joao.guerra:r-x
default:group::--x
default:mask::r-x
default:other::--x
```

Caso você queira remover permissões de acesso recursivamente para todos os arquivos e subdiretórios dentro de "pasta_compartilhada", você pode usar a opção `-R`:

```bash
setfacl -R -x u:joao.guerra /home/marie.curie/pasta_compartilhada
```

Caso você queira remover acesso para todas os arquivos e subdiretórios que podem ser criados dentro de "pasta_compartilhada", você pode usar a opção `-d`:

```bash
setfacl -d -x u:joao.guerra /home/marie.curie/pasta_compartilhada
```

Então, cheque novamente as mudanças com o comando `getfacl`:

```bash
$ getfacl /home/marie.curie/pasta_compartilhada
# file: /home/marie.curie/pasta_compartilhada
# owner: marie.curie
# group: domain\040users
user::rwx
group::--x
mask::--x
other::--x
default:user::rwx
default:group::--x
default:mask::--x
default:other::--x
```

Para remover todas as permissões de acesso, você pode usar o comando `setfacl -b` seguido do caminho do diretório. Por exemplo, para remover todas as permissões de acesso no diretório "pasta_compartilhada", use o comando:

```bash
setfacl -b /home/marie.curie/pasta_compartilhada
```

Então, cheque novamente as mudanças com o comando `getfacl`:

```bash
$ getfacl /home/marie.curie/pasta_compartilhada
# file: /home/marie.curie/pasta_compartilhada
# owner: marie.curie
# group: domain\040users
user::rwx
group::--x
other::--x
```

## Usando links simbólicos para pastas compartilhadas

Para facilitar o acesso a pastas compartilhadas, você pode criar links simbólicos (atalhos) para essas pastas em seu `HOME`. Isso é especialmente útil quando você precisa acessar frequentemente uma pasta compartilhada sem precisar navegar até o caminho completo toda vez.

Para criar um link simbólico, você pode usar o comando `ln -s` seguido do caminho da pasta compartilhada e do caminho onde deseja criar o link. Por exemplo, se você quiser criar um link simbólico para a pasta compartilhada `/shared/groups/edb` no seu diretório `HOME`, você pode usar o seguinte comando:

```bash
ln -s /shared/groups/edb /home/marie.curie/edb
```

<div class="warning">
Programas que estão instalados via singularity podem não ter acesso a pastas compartilhadas. Para resolver isso, você pode usar o comando <code>singularity run --bind /caminho/da/pasta/compartilhada:/caminho/dentro/do/container imagem.sif</code>.
</div>

## Referências adicionais

- [An introduction to Linux Access Control Lists (ACLs)](https://www.redhat.com/sysadmin/linux-access-control-lists)
- [Red Hat Docs - Chapter25. Managing file permissions](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_basic_system_settings/assembly_managing-file-permissions_configuring-basic-system-settings)
- [Red Hat Docs - Chapter 28. Managing the Access Control List](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_basic_system_settings/assembly_managing-access-control-list_configuring-basic-system-settings)
- [Arch Linux Wiki - Access Control Lists (Português)](https://wiki.archlinux.org/title/Access_Control_Lists_(Portugu%C3%AAs))
- [Using ACLs](https://web.archive.org/web/20191220012518/http://vanemery.net:80/Linux/ACL/linux-acl.html)
