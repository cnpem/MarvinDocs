# seqtk

O [seqtk](https://github.com/lh3/seqtk) é um conjunto de ferramentas leves em linha de comando para o processamento rápido de arquivos FASTA e FASTQ. Desenvolvido em C, ele é altamente eficiente e indicado para tarefas comuns de manipulação de sequências, como conversão entre formatos, amostragem aleatória, filtragem, recorte, cálculo de estatísticas e reversão de sequências. O seqtk é amplamente utilizado em pipelines de bioinformática por sua velocidade, simplicidade e fácil integração com outros utilitários de linha de comando.  

Para mais informações e documentação completa, acesse: <https://github.com/lh3/seqtk/tree/master>

## Carregando o módulo

Para habilitar o seqtk no HPCC Marvin, você deve carregar o módulo `seqtk`:

```bash
module load seqtk
```

<div class="warning">
    <br>As versões disponíveis do seqtk no HPCC Marvin são:
    <ul>
        <li><code>seqtk/1.5   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help seqtk
```

## Executando o módulo

Modelo de uso do seqtk via linha de comando:

```bash
seqtk [OPTIONS] COMMAND [ARGS]...
```

Ao executar `seqtk -h`, é possível consultar a lista de comandos disponíveis:

```text
Command: 
  seq       common transformation of FASTA/Q
  size      report the number sequences and bases
  comp      get the nucleotide composition of FASTA/Q
  sample    subsample sequences
  subseq    extract subsequences from FASTA/Q
  fqchk     fastq QC (base/quality summary)
  mergepe   interleave two PE FASTA/Q files
  split     split one file into multiple smaller files
  trimfq    trim FASTQ using the Phred algorithm

  hety      regional heterozygosity
  gc        identify high- or low-GC regions
  mutfa     point mutate FASTA at specified positions
  mergefa   merge two FASTA/Q files
  famask    apply a X-coded FASTA to a source FASTA
  dropse    drop unpaired from interleaved PE FASTA/Q
  rename    rename sequence names
  randbase  choose a random base from hets
  cutN      cut sequence at long N
  gap       get the gap locations
  listhet   extract the position of each het
  hpc       homopolyer-compressed sequence
  telo      identify telomere repeats in asm or long reads
```

Para mais detalhes sobre os parâmetros de cada comando do seqtk, use:

```bash
seqtk [COMMAND] -h
```

Também consulte os exemplos de uso no [repositório do seqtk](https://github.com/lh3/seqtk/blob/master/README.md).

## Submetendo jobs

A execução do seqtk no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `seqtk.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=seqtk
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --mem-per-cpu=2GB

module load seqtk/1.5

INPUT_FASTQ="/caminho/para/input.fq.gz"
OUTPUT_FASTA="/caminho/para/output.fa"

# Convert FASTQ to FASTA
seqtk seq -a "$INPUT_FASTQ" >  "$OUTPUT_FASTA"
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch seqtk.sh
```
