# deepTools

O [deepTools](https://deeptools.readthedocs.io/en/latest/index.html) é um **conjunto de ferramentas para análise e visualização de dados de sequenciamento de próxima geração (NGS)**, especialmente voltado para **experimentos baseados em alinhamentos** como ChIP-seq, RNA-seq e ATAC-seq.  

Ele oferece utilitários para **normalizar, comparar e representar graficamente** dados em formato BAM, bigWig ou bedGraph, permitindo análises detalhadas de cobertura genômica, perfis de enriquecimento e padrões epigenéticos.  

O deepTools é amplamente utilizado em **bioinformática e genômica funcional** para explorar relações entre marcas epigenéticas, expressão gênica e estrutura cromatínica.  

Para mais informações, acesse: <https://deeptools.readthedocs.io/en/latest/index.html>

## Carregando o módulo

Para habilitar o deeptools no HPCC Marvin, você deve carregar o módulo `deeptools`:

```bash
module load deeptools
```

<div class="warning">
    <br>As versões disponíveis do deeptools no HPCC Marvin são:
    <ul>
        <li><code>deeptools/3.5.6   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help deeptools
```

## Executando o módulo

O deeptools consiste em diversas ferramentas que podem ser chamadas pelo próprio nome, por exemplo:

```bash
multiBamSummary bins --bamfiles file1.bam file2.bam -o results.npz 
```

Algumas outras ferramentas são:

```text
findRestSite                 Identifies the genomic locations of restriction sites
hicBuildMatrix               Creates a Hi-C matrix using the aligned BAM files of the Hi-C sequencing reads
hicQuickQC                   Estimates the quality of Hi-C dataset
hicQC                        Plots QC measures from the output of hicBuildMatrix
hicCorrectMatrix             Uses iterative correction to remove biases from a Hi-C matrix
```

Consulte todas as ferramentas disponíveis com `deeptools -h` e mais informações na [documentação oficial do deeptools](https://deeptools.readthedocs.io/en/latest/content/list_of_tools.html).

## Submetendo jobs

A execução do deeptools no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `deeptools.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=deeptools
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem-per-cpu=4GB

module load deeptools/3.5.6

BAM_FILE_1="/caminho/para/bamfile1"
BAM_FILE_2="/caminho/para/bamfile2"
OUTPUT_FILE="results.npz"

multiBamSummary bins --bamfiles "$BAM_FILE_1" "$BAM_FILE_2" -o "$OUTPUT_FILE" 
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch deeptools.sh
```

Para mais detalhes sobre os parâmetros do deeptools, use:

```bash
deeptools -h
```
