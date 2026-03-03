# OMERO Downloader

O repositório de imagens [OMERO](https://www.openmicroscopy.org/omero/) é uma plataforma para armazenamento, gerenciamento e compartilhamento de imagens científicas, especialmente de microscopia.

O OMERO Downloader é uma ferramenta de linha de comando que serve para baixar em massa imagens e metadados de um repositório OMERO, preservando a estrutura de pastas dos _datasets_ e projetos. Essa ferramenta é útil para obter cópias locais das imagens armazenadas no repositório.

Para mais informações sobre o OMERO Downloader, acesse <https://github.com/ome/omero-downloader>.

## Carregando o modulo

Para habilitar o OMERO Downloader no HPCC Marvin, você deve carregar o módulo `omero-downloader`:

```bash
module load omero-downloader
```

<div class="warning">
    <br>As versões disponíveis do OMERO Downloader no HPCC Marvin são:
    <ul>
        <li><code>omero-downloader/0.2.2  (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do módulo, use:

```bash
module help omero-downloader
```

Para acessar a documentação completa dos parâmetros do OMERO Downloader, execute:

```bash
omero-downloader --help
```

## Realizando login

O OMERO Downloader requer autenticação para acessar os dados armazenados no repositório. Porém, se passarmos os dados como usuário e senha no comando, eles estarão expostos ao analisarmos os processos em execução no sistema, o que pode representar um risco de segurança. Para evitar isso, é recomendado realizar o login usando o comando `omero login` e, em seguida, usar o OMERO Downloader passando uma chave de sessão com a opção `-k`.

Para isso, carregue o módulo do Omero CLI:

```bash
ml load omero
```

Em seguida, execute o comando de login:

```bash
omero login -s omero-lnbio.cnpem.br -u <user_name>
```

Você será solicitado a inserir senha. Após o login, uma chave de sessão será gerada e armazenada localmente. Para usar essa chave de sessão com o OMERO Downloader.

Para verificar as suas chaves de sessão, use:

```bash
omero sessions list
```

Você verá algo como isso:

```bash
$ omero sessions list
 Server               | User     | Group | Session                              | Active    | Started
----------------------+----------+-------+--------------------------------------+-----------+--------------------------
 omero-lnbio.cnpem.br | analista | LIB   | b22d1f3c-e7f3-4cb4-afea-4ce656d82dab | Logged in | Mon Mar  2 15:29:09 2026
(1 row)
```

No exemplo acima, você utilizaria a chave de sessão `b22d1f3c-e7f3-4cb4-afea-4ce656d82dab` com a opção `-k` do OMERO Downloader.


## Baixando dados

O comando base para baixar dados com o OMERO Downloader é o seguinte:

```bash
omero-downloader -b <output_dir> -k <session_key> -f <file> <type>:<ID>
```

<div class="warning">
    <br>
    Substitua as informações indicadas entre colchetes angulares (<code>&lt;...&gt;</code>):
    <ul>
        <li><code>&lt;output_dir&gt;</code>: diretório onde os dados serão baixados. É importante que a pasta já exista.</li>
        <li><code>&lt;user_name&gt;</code>: seu nome de usuário institucional, no formato <code>nome.sobrenome</code>.</li>
        <li><code>&lt;password&gt;</code>: sua senha institucional.</li>
        <li><code>&lt;file&gt;</code>: formato do arquivo a ser baixado. O formato recomendado é <code>ome-tiff</code>; outros formatos estão disponíveis na documentação de parâmetros do OMERO Downloader.</li>
        <li><code>&lt;type&gt;</code>: tipo de objeto que você deseja baixar:
            <ul>
                <li><code>Image</code>: arquivo de imagem único.</li>
                <li><code>Dataset</code>: conjunto de arquivos de imagem.</li>
                <li><code>Project</code>: conjunto de datasets.</li>
            </ul>
        </li>
        <li><code>&lt;ID&gt;</code>: número de identificação do objeto que deseja baixar.</li>
    </ul>
</div>

Para baixar uma imagem, use:

```bash
omero-downloader -b /home/marie.curie/pasta_destino -k <session_key> -f ome-tiff Image:123
```

Para baixar um _Dataset_, use:

```bash
omero-downloader -b /home/marie.curie/pasta_destino -k <session_key> -f ome-tiff Dataset:123
```

Para baixar um projeto, use:

```bash
omero-downloader -b /home/marie.curie/pasta_destino -k <session_key> -f ome-tiff Project:123
```

<div class="warning">
    <br>Para descobrir o número de identificação (ID) de uma imagem, dataset ou projeto, acesse a plataforma 
    <a href="https://omero-lnbio.cnpem.br">https://omero-lnbio.cnpem.br</a>. 
    Nela, é possível visualizar a organização dos projetos, datasets e imagens aos quais você tem acesso. 
    Ao selecionar o item desejado, o ID correspondente será exibido no painel à direita, na guia <i>“General”</i>.<br>
</div>

