# GTDB-Tk

O [GTDB-Tk (Genome Taxonomy Database Toolkit)](https://ecogenomics.github.io/GTDBTk/) é uma ferramenta desenvolvida para classificar genomas bacterianos e arqueanos de forma padronizada com base no Genome Taxonomy Database (GTDB). Ele utiliza abordagens filogenéticas e de similaridade genômica (ANI) para atribuir classificações taxonômicas consistentes e atualizadas, garantindo maior precisão e reprodutibilidade nas análises de genomas microbianos.

O GTDB-Tk é amplamente utilizado em estudos de metagenômica e genômica comparativa, integrando-se facilmente a pipelines bioinformáticos para análise em larga escala.

Para mais informações e documentação completa, acesse: <https://ecogenomics.github.io/GTDBTk/>


## Carregando o módulo

Para habilitar o GTDB-Tk no HPCC Marvin, você deve carregar o módulo `gtdbtk`:

```bash
module load gtdbtk
```

<div class="warning">
    <br>As versões disponíveis do gtdbtk no HPCC Marvin são:
    <ul>
        <li><code>gtdbtk/2.5.2   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help gtdbtk
```

## Dados de referência

Para executar o GTDB-Tk, é necessário o download da database com dados de referência, que pesa em torno de 140G.

Atualmente, a database de referência está localizada em `/public/gtdbtk_reference_data/`.

Caso seja necessário alterar o local dos dados de referência que desejar utilizar, é necessário configurar a variável `GTDBTK_DATA_PATH` antes de executar o módulo:

```bash
export GTDBTK_DATA_PATH="/novo/path/desejado/do/reference/data/"
```

## Executando o módulo

Modelo de uso do GTDB-Tk via linha de comando:

```bash
gtdbtk COMMAND [ARGS]...
```

Ao executar `gtdbtk -h`, é possível consultar a lista de comandos disponíveis:

```text
Workflows:
  classify_wf -> Classify genomes by placement in GTDB reference tree
                    (ani_screening -> identify -> align -> classify)
  de_novo_wf  -> Infer de novo tree and decorate with GTDB taxonomy
                    (identify -> align -> infer -> root -> decorate)

Methods:
  identify -> Identify marker genes in genome
  align    -> Create multiple sequence alignment
  classify -> Determine taxonomic classification of genomes
  infer    -> Infer tree from multiple sequence alignment
  root     -> Root tree using an outgroup
  decorate -> Decorate tree with GTDB taxonomy

Tools:
  infer_ranks        -> Establish taxonomic ranks of internal nodes using RED
  ani_rep            -> Calculates ANI to GTDB representative genomes
  trim_msa           -> Trim an untrimmed MSA file based on a mask
  export_msa         -> Export the untrimmed archaeal or bacterial MSA file
  remove_labels      -> Remove labels (bootstrap values, node labels) from an Newick tree
  convert_to_itol    -> Convert a GTDB-Tk Newick tree to an iTOL tree
  convert_to_species -> Convert GTDB genome IDs to GTDB species names

Testing:
  test          -> Validate the classify_wf pipeline with 3 archaeal genomes
  check_install -> Verify third party programs and GTDB reference package
```

Consulte todos informações completas sobre os comandos na página de [referência de comandos na documentação oficial do  gtdbtk](https://ecogenomics.github.io/GTDBTk/commands/index.html).

## Submetendo jobs

A execução do GTDB-Tk no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `gtdbtk.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=gtdbtk
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=32
#SBATCH --mem-per-cpu=8GB

module load gtdbtk/2.5.2

GENOME_DIR="/caminho/para/diretorio/genoma"
OUTPUT_DIR="/caminho/para/diretorio/output"

gtdbtk classify_wf --genome-dir_ ${GENOME_DIR} --out_dir ${OUTPUT_DIR}
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch gtdbtk.sh
```

Para mais detalhes sobre os parâmetros de cada comando do GTDB-Tk, use:

```bash
gtdbtk [COMMAND] -h
```
