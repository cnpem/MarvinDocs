# OMERO Downloader

OMERO é uma plataforma para armazenar, gerenciar e compartilhar imagens científicas, especialmente de microscopia. 
OMERO Downloader é uma ferramenta de linha de comando que serve para baixar em massa imagens e metadados de um servidor OMERO, mantendo a estrutura de pastas dos projetos e datasets. 
É útil para obter cópias locais das imagens armazenadas no servidor.

Para mais informações sobre o OMERO Downloader, acesse https://github.com/ome/omero-downloader.

## Carregando o modulo

Para habilitar o OMERO Downloader no HPCC Marvin, você deve carregar o módulo `omero-downloader`:
```
module load omero-downloader
```

Para acessar a documentação do módulo, utilize:
```
module help omero-downloader
```

Para acessar a documentação do própria dos parametros do OMERO Downloader utilize:
```
omero-downloader --help
```

## Baixando dados

A seguir esta o comando base para baixar dados atraves do OMERO Downloader, substitua as informações nos trechos entre os colchetes angulares (`<...>`):

```
omero-downloader -b <output dir> -s omero-lnbio.cnpem.br -u <user name> -w <password> -f <file> <type>:<image ID>
```
- `<output dir>`: pasta onde o dado sera baixado. É importante que a pasta ja exista.
- `<user name>`: seu usuário, ou seja, `nome.sobrenome`.
- `<password>`: sua senha institucional.
- `<file>`: formato que sera baixado. O formato recomendado é o "ome-tiff", os outros formatos estão disponiveis na documentação de parametros do OMERO Downloader.
- `<type>`: tipo de objeto que você deseja baixar:
    - `Image`: Arquivo de imagem único.
    - `Dataset`: Grupo de arquivos de imagens.
    - `Project`: Grupo de Datasets.
- `<ID>`: número de identificação do objeto que deseja baixar.

Veja três exemplos de código para baixar uma imagem, um Dataset e um projeto, respectivamente:

```
omero-downloader -b /home/joao.santos/pasta_destino -s omero-lnbio.cnpem.br -u joao.santos -w minhasenha123 -f ome-tiff Image:12345678
```

```
omero-downloader -b /home/joao.santos/pasta_destino -s omero-lnbio.cnpem.br -u joao.santos -w minhasenha123 -f ome-tiff Image:123
```

```
omero-downloader -b /home/joao.santos/pasta_destino -s omero-lnbio.cnpem.br -u joao.santos -w minhasenha123 -f ome-tiff Image:123
```

<div class="warning">
    <br><b>Dica:</b> uma forma de descobrir qual o número de identificação (ID) do objeto é através da plataforma https://omero-lnbio.cnpem.br/webclient, nela você pode vizualizar a organização dos projetos, bases de dados, e imagens que tem acesso.
    Ao selecionar o que deseja, o ID irá aparecer ao lado direito na guia <i>"General"</i>.<br>
</div>
