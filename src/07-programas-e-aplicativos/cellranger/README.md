# Cellranger

O [Cellranger](https://www.10xgenomics.com/support/software/cell-ranger/latest) é um conjunto de pipelines de análise desenvolvido pela 10x Genomics para processar dados de sequenciamento de célula única (*single-cell*). Ele realiza o alinhamento de leituras, atribuição de barcodes, contagem de identificadores moleculares únicos (UMIs) e análise de expressão gênica.

Para mais informações e documentação completa, acesse: <https://www.10xgenomics.com/support/software/cell-ranger/latest/getting-started>.

## Carregando o módulo

Para habilitar o Cellranger no HPCC Marvin, você deve carregar o módulo `cellranger`:

```bash
module load cellranger
```

<div class="warning">
    <br>As versões disponíveis do cellranger no HPCC Marvin são:
    <ul>
        <li><code>cellranger/10.0.0   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help cellranger
```

## Executando o módulo

Modelo de uso do Cellranger via linha de comando:

```bash
cellranger <COMMAND>
```

Ao executar `cellranger -h`, é possível consultar a lista de comandos disponíveis:

```text
cellranger 10.0.0

Process 10x Genomics Gene Expression, Feature Barcode, and Immune Profiling data

Usage: cellranger <COMMAND>

Commands:
  count           Count gene expression and/or feature barcode reads from a single sample and GEM well
  multi           Analyze multiplexed data or combined gene expression/immune profiling/feature barcode data
  multi-template  Output a multi config CSV template
  vdj             Assembles single-cell VDJ receptor sequences from 10x Immune Profiling libraries
  aggr            Aggregate data from multiple Cell Ranger runs
  annotate        Annotate cell-types from outputs of a CellRanger run
  reanalyze       Re-run secondary analysis (dimensionality reduction, clustering, etc)
  mkvdjref        Prepare a reference for use with CellRanger VDJ
  mkfastq         Run Illumina demultiplexer on sample sheets that contain 10x-specific sample index sets
  testrun         Execute the 'count' pipeline on a small test dataset
  cloud           Invoke cloud commands
  mat2csv         Convert a feature-barcode matrix to CSV format
  mkref           Prepare a reference for use with 10x analysis software. Requires a GTF and FASTA
  mkgtf           Filter a GTF file by attribute prior to creating a 10x reference
  upload          Upload analysis logs to 10x Genomics support
  sitecheck       Collect Linux system configuration information
  telemetry       Configure and inspect telemetry settings and data
  help            Print this message or the help of the given subcommand(s)

Options:
  -h, --help     Print help
  -V, --version  Print version
```

Para mais detalhes sobre os parâmetros de cada comando do Cellranger, use:

```bash
cellranger help [COMMAND]
```

## Arquivos de referência

O Cellranger requer arquivos de referência (como genomas, transcriptomas e índices de amostras) para a execução das análises. No HPCC Marvin, essas referências oficiais (obtidas diretamente da [página de downloads do Cellranger](https://www.10xgenomics.com/support/software/cell-ranger/downloads)) já estão centralizadas e prontas para uso no seguinte diretório: `/public/cellranger`.

Para otimizar o espaço do cluster e evitar redundâncias, não recomendamos o armazenamento de cópias de arquivos de referência em diretórios pessoais (como o seu `/home`). Caso a sua análise exija uma referência ou genoma customizado que ainda não esteja disponível no diretório público, por favor, entre em contato com a equipe da EDB.

Atualmente, essa é a estrutura dos dados de referência do Cellranger:

```bash
/public/cellranger
├── probe-sets
│   ├── barcode-sequence
│   │   └── flex-v2-384.txt
│   └── human-transcriptome
│       ├── Chromium_Human_Transcriptome_Probe_Set_v2.0.0_GRCh38-2024-A.bed
│       ├── Chromium_Human_Transcriptome_Probe_Set_v2.0.0_GRCh38-2024-A.csv
│       ├── Chromium_Human_Transcriptome_Probe_Set_v2.0.0_GRCh38-2024-A.offtarget.csv
│       └── Chromium_Human_Transcriptome_Probe_Set_v2.0.0_GRCh38-2024-A.probe_metadata.tsv
├── references
│   └── human
│       └── refdata-gex-GRCh38-2024-A
│           ├── fasta
│           │   ├── genome.fa
│           │   └── genome.fa.fai
│           ├── genes
│           │   └── genes.gtf.gz
│           ├── reference.json
│           └── star
│               ├── chrLength.txt
│               ├── chrNameLength.txt
│               ├── chrName.txt
│               ├── chrStart.txt
│               ├── exonGeTrInfo.tab
│               ├── exonInfo.tab
│               ├── geneInfo.tab
│               ├── Genome
│               ├── genomeParameters.txt
│               ├── SA
│               ├── SAindex
│               ├── sjdbInfo.txt
│               ├── sjdbList.fromGTF.out.tab
│               ├── sjdbList.out.tab
│               └── transcriptInfo.tab
└── sample-index-sequences
    ├── Chromium-i7-Multiplex-Kit-N-Set-A-sample-indexes-plate.csv
    ├── Chromium-i7-Multiplex-Kit-N-Set-A-sample-indexes-plate.json
    ├── chromium-shared-sample-indexes-plate-5.csv
    ├── chromium-shared-sample-indexes-plate-5.json
    ├── chromium-shared-sample-indexes-plate.csv
    ├── chromium-shared-sample-indexes-plate.json
    ├── chromium-single-cell-sample-indexes-plate-v1.csv
    ├── chromium-single-cell-sample-indexes-plate-v1.json
    ├── gemcode-single-cell-sample-indexes-plate.csv
    └── gemcode-single-cell-sample-indexes-plate.json

10 directories, 34 files
```


## Submetendo jobs

A execução do cellranger no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `cellranger.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=cellranger
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=16
#SBATCH --mem-per-cpu=4GB

module load cellranger

ID="sample1"
TRANSCRIPTOME="/public/cellranger/references/human/refdata-gex-GRCh38-2024-A"
FASTQS_DIR="/caminho/para/fastq_dir"
SAMPLE="SA001"      # prefixo dos arquivos fastq

cellranger count --id="$ID" \
                 --transcriptome="$TRANSCRIPTOME" \
                 --fastqs="$FASTQS_DIR" \
                 --sample="$SAMPLE" \
                 --create-bam=true
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch cellranger.sh
```
