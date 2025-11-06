# Trimmomatic

O [Trimmomatic](http://www.usadellab.org/cms/?page=trimmomatic) é uma ferramenta em linha de comando amplamente utilizada para o pré-processamento de dados de sequenciamento de DNA provenientes de plataformas Illumina. Ela realiza etapas fundamentais de limpeza das leituras (reads), incluindo remoção de adaptadores, filtragem por qualidade, corte de regiões de baixa qualidade e eliminação de leituras curtas, garantindo que apenas dados de alta confiabilidade sejam utilizados em análises posteriores. Altamente flexível e eficiente, suporta tanto dados single-end quanto paired-end, além de permitir o ajuste fino de parâmetros conforme o protocolo experimental.

Para mais informações, acesse: <https://github.com/usadellab/Trimmomatic>.

## Carregando o módulo

Para habilitar o trimmomatic no HPCC Marvin, você deve carregar o módulo `trimmomatic`:

```bash
module load trimmomatic
```

<div class="warning">
    <br>As versões disponíveis do trimmomatic no HPCC Marvin são:
    <ul>
        <li><code>trimmomatic/0.4   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help trimmomatic
```

## Executando o módulo

Há dois modos de executar o trimmomatic, **SE (Singe End)** para leituras únicas, e **PE (Paired End)** para leituras emparelhadas.

### Single end 

Como executar o módulo no modo SE:

```bash
trimmomatic SE [-threads <threads>] [-phred33 | -phred64] [-trimlog <logFile>] <input> <output> <step 1> ...
```

Exemplo:

```bash
trimmomatic SE -threads 4 input.fastq.gz output_trimmed.fastq.gz \
  ILLUMINACLIP:TruSeq3-SE.fa:2:30:10 SLIDINGWINDOW:4:20 MINLEN:36
```

### Paired end

Como executar o módulo no modo PE:

```bash
trimmomatic PE [-threads <threads>] [-phred33 | -phred64] [-trimlog <logFile>] >] [-basein <inputBase> | <input 1> <input 2>] [-baseout <outputBase> | <unpaired output 1> <paired output 2> <unpaired output 2> <step 1> ...
```

Exemplo:

```bash
trimmomatic PE -threads 8 input_R1.fastq.gz input_R2.fastq.gz \
  output_R1_paired.fastq.gz output_R1_unpaired.fastq.gz \
  output_R2_paired.fastq.gz output_R2_unpaired.fastq.gz \
  ILLUMINACLIP:TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 MINLEN:36
```

Consulte as informações completas sobre os comandos e opções do módulo no [repositório oficial do trimmomatic no GitHub](https://github.com/usadellab/Trimmomatic) e também no [manual em pdf (versão 0.32)](http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf).

## Submetendo jobs

A execução do trimmomatic no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `trimmomatic.sh`, com o seguinte conteúdo:
u
```bash
#!/bin/bash
#SBATCH --job-name=trimmomatic
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem=8G

INPUT_R1="reads_R1.fastq.gz"
INPUT_R2="reads_R2.fastq.gz"
OUTPUT_R1_PAIRED="reads_R1_paired.fastq.gz"
OUTPUT_R1_UNPAIRED="reads_R1_unpaired.fastq.gz"
OUTPUT_R2_PAIRED="reads_R2_paired.fastq.gz"
OUTPUT_R2_UNPAIRED="reads_R2_unpaired.fastq.gz"
ADAPTERS="path/to/adapters/TruSeq3-PE.fa"

module load trimmomatic/0.4

trimmomatic PE -threads ${SLURM_CPUS_PER_TASK} \
  $INPUT_R1 $INPUT_R2 \
  $OUTPUT_R1_PAIRED $OUTPUT_R1_UNPAIRED \
  $OUTPUT_R2_PAIRED $OUTPUT_R2_UNPAIRED \
  ILLUMINACLIP:${ADAPTERS}:2:30:10 SLIDINGWINDOW:4:20 MINLEN:36
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch trimmomatic.sh
```
