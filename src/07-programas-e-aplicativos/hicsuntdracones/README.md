# HiCsuntdracones

O [HiC-sunt-dracones](https://github.com/ComputationalEpigenetics/hic-sunt-dracones) é um software para **análise e comparação de dados Hi-C** em larga escala.  
Ele foi desenvolvido para identificar **diferenças estruturais na organização tridimensional do genoma** entre condições ou tipos celulares distintos.

A ferramenta realiza o pré-processamento, normalização e detecção de regiões diferencialmente organizadas (DORs), permitindo avaliar alterações em domínios topológicos (TADs) e padrões de interação cromossômica.  

O HiC-sunt-dracones é amplamente utilizado em estudos de epigenômica e arquitetura nuclear, fornecendo uma abordagem estatística robusta para comparar dados Hi-C entre múltiplas amostras.  

Para mais informações, acesse: <https://github.com/ComputationalEpigenetics/hic-sunt-dracones>

## Carregando o módulo

Para habilitar o hicsuntdracones no HPCC Marvin, você deve carregar o módulo `hicsuntdracones`:

```bash
module load hicsuntdracones
```

<div class="warning">
    <br>As versões disponíveis do hicsuntdracones no HPCC Marvin são:
    <ul>
        <li><code>hicsuntdracones/0.2.0   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help hicsuntdracones
```

## Executando o módulo

Após carregar o hicsuntdracones, ele pode ser executado tanto com sua abreviação `hicsd`, como com seu nome completo `hicsuntdracones`.

O consiste em diversos comandos, por exemplo:

```bash
hicsd  hicpro2homer [-h] --input_bed INPUT_BED --input_matrix INPUT_MATRIX --output_matrix OUTPUT_MATRIX
```

Lista completa dos comandos:

```text
version             Show version
hicpro2homer        Convert a matrix in HiC-Pro format to Homer format
mHiC2homer          Convert a matrix in mHiC format to Homer format
number_of_bins      Return the number of bins of the matrix
chromosomes         Return the chromosomes used in the matrix
norm_by_col_sum     Normalize by column sum to make matrices comparable
submatrix           Extract submatrices
diff_matrix         Generate differential matrix by dividing the values of one matrix by the values of the other.
heatmap             Plot interaction matix heatmap
histogram           Plot histogram for matrix reads
virtual_4C          Perform virtual 4C analysis
dist_dep_decay      Distant dependent decay
colo                Perform colocalisation analysis
colo_diff           Perform differential colocalisation analysis
ploidy              Apply ploidy factors

```

Consulte todas as ferramentas disponíveis com `hicsd -h`.

## Submetendo jobs

A execução do hicsuntdracones no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `hicsuntdracones.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=hicsuntdracones
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem-per-cpu=4GB

module load hicsuntdracones/0.2.0

INPUT_BED="/caminho/para/input/bed"
INPUT_MATRIX="/caminho/para/input/matrix"
OUTPUT_MATRIX="/caminho/para/output/matrix"

hicsd hicpro2homer [-h] --input_bed INPUT_BED --input_matrix INPUT_MATRIX --output_matrix OUTPUT_MATRIX
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch hicsuntdracones.sh
```

Para mais detalhes sobre os parâmetros do HiCsuntdracones, use:

```bash
hicsuntdracones -h
```
