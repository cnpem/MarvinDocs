# OMERO CLI

O OMERO-CLI é um conjunto de ferramentas de linha de comando baseado em Python, feito para interagir com servidores OMERO. Ele permite que os usuários realizem várias operações, como autenticação, upload/download, import/export, gerenciamento de dados e muito mais, diretamente do terminal.

Para mais informações, acesse a documentação oficial do OMERO-CLI em <https://omero.readthedocs.io/en/stable/users/cli/overview.html>.

## Carregando o módulo

Para habilitar o OMERO-CLI no HPCC Marvin, você deve carregar o módulo `omero`:

```bash
module load omero
```

<div class="warning">
    <br>As versões disponíveis do OMERO-CLI no HPCC Marvin são:
    <ul>
        <li><code>omero/5.22  (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do módulo, use:

```bash
module help omero
```

Para acessar a documentação completa dos parâmetros do OMERO Downloader, execute:

```bash
omero --help
```

## Realizando login

O OMERO-CLI requer autenticação para acessar os dados armazenados no repositório. Para realizar o login, use o comando `omero login`:

```bash
omero login
```

Dados como servidor, usuário e senha serão solicitados interativamente. Você também pode passar todos eles como argumentos para evitar a solicitação interativa:

```bash
omero login -s omero-lnbio.cnpem.br -u <user_name> -w <senha>
```

## Autenticando para o OMERO Downloader

O OMERO Downloader requer autenticação para acessar os dados armazenados no repositório. Porém, se passarmos os dados como usuário e senha no comando, eles estarão expostos ao analisarmos os processos em execução no sistema, o que pode representar um risco de segurança. Para evitar isso, é recomendado realizar o login usando o comando `omero login` e, em seguida, usar o OMERO Downloader passando uma chave de sessão com a opção `-k`.

Após o login, uma chave de sessão será gerada e armazenada localmente. Para usar essa chave de sessão com o OMERO Downloader, você pode verificar as suas chaves de sessão usando:

```bash
omero sessions list
```

Para mais detalhes, consulte a página de documentação do [OMERO Downloader](/src/07-programas-e-aplicativos/omero-downloader/README.md).

