# Cooler

O [Cooler](https://github.com/open2c/cooler) é uma ferramenta e biblioteca Python para **armazenar, manipular e acessar matrizes de contato Hi-C** de forma eficiente.  
Ele utiliza o formato `.cool`, baseado em HDF5, que permite consultas rápidas e armazenamento compacto de dados de interação cromossômica.

O Cooler fornece tanto **utilitários de linha de comando** quanto **interfaces Python**, possibilitando a criação, indexação e análise de dados Hi-C em diferentes resoluções.  

Para mais informações, acesse: <https://cooler.readthedocs.io/en/stable/>

## Carregando o módulo

Para habilitar o cooler no HPCC Marvin, você deve carregar o módulo `cooler`:

```bash
module load cooler
```

<div class="warning">
    <br>As versões disponíveis do cooler no HPCC Marvin são:
    <ul>
        <li><code>cooler/0.10.4   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help cooler
```

## Executando o módulo

O pacote cooler incluí diversos comandos que são utilizados no para criar, realizar queries e manipular arquivos cooler.
Modelo de uso do cooler via linha de comando:

```bash
cooler [OPTIONS] COMMAND [ARGS]...
```

Ao executar `cooler -h`, é possível consultar a lista de comandos disponíveis:

```text
Commands:
  balance   Out-of-core matrix balancing.
  cload     Create a cooler from genomic pairs and bins.
  coarsen   Coarsen a cooler to a lower resolution.
  csort     Sort and index a contact list.
  digest    Generate fragment-delimited genomic bins.
  dump      Dump a cooler's data to a text stream.
  ls        List all coolers inside a file.
  cp        Copy a cooler from one file to another or within the same file.
  ln        Create a hard link to a cooler (rather than a true copy) in...
  mv        Rename a cooler within the same file.
  tree      Display a file's data hierarchy.
  attrs     Display a file's attribute hierarchy.
  info      Display a cooler's info and metadata.
  load      Create a cooler from a pre-binned matrix.
  makebins  Generate fixed-width genomic bins.
  merge     Merge multiple coolers with identical axes.
  show      Display and browse a cooler in matplotlib.
  zoomify   Generate a multi-resolution cooler file by coarsening.
```

Consulte todos informações completas sobre os comandos na página de [referência de CLI na documentação oficial do cooler](https://cooler.readthedocs.io/en/stable/cli.html).

## Submetendo jobs

A execução do cooler no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `cooler.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=cooler
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem-per-cpu=4GB

module load cooler/0.10.4

BINS="/caminho/para/bed/file"
PAIRS_PATH="/caminho/para/contacts/file"
COOL_PATH="/caminho/para/output/cool/file"

cooler cload pairs "$BINS" "$PAIRS_PATH" "$COOL_PATH"
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch cooler.sh
```

Para mais detalhes sobre os parâmetros de cada comando do cooler, use:

```bash
cooler [COMMAND] -h
```
