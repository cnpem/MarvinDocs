# Transferência de dados

O HPCC Marvin oferece várias opções para transferir dados entre o sistema e seu computador local. As principais ferramentas para essa tarefa são: SFTP, SCP e Rsync.

## SSH File Transfer Protocol (SFTP)

O [SFTP](https://linux.die.net/man/1/sftp) é um protocolo seguro que permite a transferência de arquivos entre sistemas operacionais diferentes. É útil quando você precisa transferir arquivos de forma segura. Para usar o SFTP, execute o seguinte comando:

   ```bash
   sftp <seu.login.cnpem>@marvin.cnpem.br
   ```

Após se conectar, você pode usar comandos como:

- `ls`: lista os arquivos no diretório atual;
- `cd`: navega para um diretório específico;
- `put`: envia um arquivo do seu computador local para o HPCC Marvin;
- `get`: baixa um arquivo do HPCC Marvin para o seu computador local.

## Secure Copy Protocol (SCP)

O [SCP](https://linux.die.net/man/1/scp) (Secure Copy Protocol) é outro protocolo seguro que usa a criptografia SSH para transferir arquivos. Ele é semelhante ao SFTP, mas é mais simples de usar e não tem recursos de navegação.

Para transferir um arquivo (e.g., `file.txt`) do seu computador local para o HPCC Marvin, use o comando:

```bash
scp file.txt <seu.login.cnpem>@marvin.cnpem.br:/caminho/de/destino/
```

Para transferir um diretório (e.g., `directory/`) do seu computador local para o HPCC Marvin, use o comando:

```bash
scp -r directory/ <seu.login.cnpem>@marvin.cnpem.br:/caminho/de/destino/
```

Para transferir um arquivo (e.g., `file.txt`) do HPCC Marvin para o seu computador local, use o comando:

```bash
scp <seu.login.cnpem>@marvin.cnpem.br:/caminho/do/arquivo/file.txt /caminho/local/de/destino/
```

Para transferir um diretório (e.g., `directory/`) do HPCC Marvin para o seu computador local, use o comando:

```bash
scp -r <seu.login.cnpem>@marvin.cnpem.br:/caminho/do/diretorio/directory/ /caminho/local/de/destino/
```

<div class="warning">
Para os usuários do Windows, o SCP pode ser usado através do
<a href="winscp.net" target="_blank">WinSCP</a>, que é uma ferramenta gráfica que facilita a transferência de arquivos via SCP.
</div>

## Rsync

O [Rsync](https://linux.die.net/man/1/rsync) é um protocolo de transferência de arquivos que pode sincronizar diretórios entre hosts. Ele usa uma conexão segura SSH e é útil para transferir grandes quantidades de dados ou sincronizar arquivos entre sistemas.

Para transferir um arquivo (e.g., `file.txt`) do seu computador local para o HPCC Marvin, use o comando:

```bash
rsync -avz file.txt <seu.login.cnpem>@marvin.cnpem.br:/caminho/de/destino/
```

Para transferir um diretório (e.g., `directory/`) do seu computador local para o HPCC Marvin, use o comando:

```bash
rsync -avz file.txt <seu.login.cnpem>@marvin.cnpem.br:/caminho/de/destino/
```

Para transferir um arquivo (e.g., `file.txt`) do HPCC Marvin para o seu computador local, use o comando:

```bash
rsync -avz <seu.login.cnpem>@marvin.cnpem.br:/caminho/do/arquivo/file.txt /caminho/local/de/destino/
```

Para transferir um diretório (e.g., `directory/`) do HPCC Marvin para o seu computador local, use o comando:

```bash
rsync -avz <seu.login.cnpem>@marvin.cnpem.br:/caminho/do/diretorio/directory/ /caminho/local/de/destino/
```

<div class="warning">
A flag <code>-a</code> mantém as permissões de arquivos, a flag <code>-v</code> mostra o progresso da transferência e a flag <code>-z</code> comprime os dados antes de transferi-los.
</div>
