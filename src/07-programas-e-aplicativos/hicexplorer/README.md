# HiCExplorer

O [HiCExplorer](https://hicexplorer.readthedocs.io/en/latest/) é um conjunto de ferramentas para **análise, processamento e visualização de dados de experimentos Hi-C**, que investigam a **organização tridimensional do genoma**.  

Ele permite construir e normalizar matrizes de contato, corrigir vieses técnicos, identificar domínios topológicos (TADs) e gerar visualizações de alta qualidade, como mapas de calor e comparações entre amostras.  

O HiCExplorer é amplamente utilizado em estudos de arquitetura genômica, regulação gênica e epigenética.  

Para mais informações, acesse: <https://hicexplorer.readthedocs.io/en/latest/>

## Carregando o módulo

Para habilitar o hicexplorer no HPCC Marvin, você deve carregar o módulo `hicexplorer`:

```bash
module load hicexplorer
```

<div class="warning">
    <br>As versões disponíveis do hicexplorer no HPCC Marvin são:
    <ul>
        <li><code>hicexplorer/3.7.6   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help hicexplorer
```

## Executando o módulo

O HiCExplorer consiste em diversas ferramentas que podem ser chamadas pelo próprio nome, por exemplo:

```bash
hicPlotMatrix -m hic_matrix.h5 -o plot.pdf
```

Algumas outras ferramentas são:

```
findRestSite                 Identifies the genomic locations of restriction sites
hicBuildMatrix               Creates a Hi-C matrix using the aligned BAM files of the Hi-C sequencing reads
hicQuickQC                   Estimates the quality of Hi-C dataset
hicQC                        Plots QC measures from the output of hicBuildMatrix
hicCorrectMatrix             Uses iterative correction to remove biases from a Hi-C matrix
```
Consulte todas as ferramentas disponíveis com `hicexplorer -h` e mais informações na [documentação oficial do hicexplorer](https://hicexplorer.readthedocs.io/en/latest/content/list-of-tools.html).

## Submetendo jobs

A execução do HiCExplorer no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `hicexplorer.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=hicexplorer
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem-per-cpu=4GB

module load hicexplorer/3.7.6

INPUT_MATRIX="/caminho/para/matriz"
OUTPUT="/caminho/para/output/desejado"

hicPlotMatrix -m "$INPUTMATRIX" -o "$OUTPUT"
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch hicexplorer.sh
```

Para mais detalhes sobre os parâmetros do Circos, use:

```bash
hicexplorer -h
```
