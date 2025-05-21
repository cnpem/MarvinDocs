# Gerenciamento de Dados

Este capítulo aborda as estratégias de gerenciamento de dados para o cluster HPC Marvin, incluindo as melhores práticas para armazenamento, transferência e backup de dados.

## Armazenamento de Dados 🗃️

O HPC Marvin fornece armazenamento em disco para os usuários. Este tópico apresenta informações sobre as opções de armazenamento disponíveis e as melhores práticas para gerenciamento de dados. Serão discutidos os seguintes tópicos:

- Opções de armazenamento: disco local e compartilhado.
- Montagem e desmontagem de sistemas de arquivos.
- Práticas recomendadas de gerenciamento de espaço em disco.
- Gerenciamento de permissões de acesso a arquivos.

## Transferência de Arquivos 📁🔄💻

Para começar a utilizar o HPC Marvin, é necessário transferir seus arquivos para o sistema. Para transferir seus arquivos, use os comandos:

1. [SFTP](https://linux.die.net/man/1/sftp) (SSH File Transfer Protocol): O SFTP é um protocolo seguro que usa a criptografia SSH para transferir arquivos. Ele é útil quando você precisa transferir arquivos entre sistemas operacionais diferentes ou quando a transferência precisa ser segura. Para transferir um arquivo usando SFTP

```bash
sftp <seu.login.cnpem>@marvin.cnpem.br
```

Isso irá se conectar ao host especificado como o usuário especificado. Uma vez conectado, você pode usar comandos como `ls`, `cd`, `put` e `get` para listar, navegar e transferir arquivos.

2. [SCP](https://linux.die.net/man/1/scp) (Secure Copy Protocol)[^2]: SCP é outro protocolo seguro que usa a criptografia SSH para transferir arquivos. Ele é semelhante ao SFTP, mas é mais simples de usar e não tem recursos de navegação.

Para transferir um arquivo usando SCP, use o comando:

```bash
scp file.txt <seu.login.cnpem>@marvin.cnpem.br:/caminho/de/destino/
```

Para transferir um diretório usando SCP, use o comando:

```bash
scp -r directory/ <seu.login.cnpem>@marvin.cnpem.br:/caminho/de/destino/
```

Isso irá copiar o arquivo `file.txt` e o diretório `directory` para o diretório especificado no HPC Marvin (marvin.cnpem.br) pelo login do usuário.

3. [Rsync](https://linux.die.net/man/1/rsync): O Rsync é um protocolo de transferência de arquivos que pode sincronizar diretórios entre hosts. Ele usa uma conexão segura SSH e é útil para transferir grandes quantidades de dados ou sincronizar arquivos entre sistemas. Para usar o Rsync, use o comando:

```bash
rsync -avz origem/ <seu.login.cnpem>@marvin.cnpem.br:/caminho/de/destino/
```

Isso irá sincronizar o diretório source com o diretório destination no host especificado como o usuário especificado. O `-a` mantém as permissões de arquivos, o `-v` mostra o progresso da transferência e o `-z` comprime os dados antes de transferi-los.

## Backup de Dados 💾

O backup de dados é essencial para garantir a integridade dos dados armazenados no HPC Marvin. Este tópico aborda as melhores práticas para backup de dados, incluindo:

- Opções de backup disponíveis.
- Como agendar backups regulares.
- Gerenciamento de restauração de dados.

Esperamos que este capítulo ajude você a gerenciar seus dados de forma eficiente e segura no HPC Marvin. Se você tiver alguma dúvida ou feedback sobre o conteúdo deste manual, não hesite em entrar em contato conosco.
