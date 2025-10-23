# Pairix

O [Pairix](https://github.com/4dn-dcic/pairix) é uma ferramenta para **indexação e consulta eficiente de arquivos `.pairs`**, usados em análises de dados **Hi-C** e genômica estrutural.  

Baseado no **Tabix**, o Pairix permite **buscas rápidas por intervalos genômicos** em arquivos de pares, suportando consultas por uma ou duas regiões genômicas.  

É amplamente utilizado em pipelines de análise e visualização de dados de interação cromossômica.  

Para mais informações, acesse: <https://github.com/4dn-dcic/pairix>

## Carregando o módulo

Para habilitar o pairix no HPCC Marvin, você deve carregar o módulo `pairix`:

```bash
module load pairix
```

<div class="warning">
    <br>As versões disponíveis do pairix no HPCC Marvin são:
    <ul>
        <li><code>pairix/0.3.9   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help pairix
```

## Executando o módulo

Além do executável `pairix`, o módulo contém outros binários auxiliares como `bgzip`, `pairs_merger` e `streamer_1d`. Execute-os para ter mais detalhes sobre o uso e parâmetros necessários e opcionais.

Exemplos de utilização do pairix para indexar:

```bash
pairix textfile.gz  # for recognized file extension
pairix -p <preset> textfile.gz
pairix -s<chr1_column> [-d<chr2_column>] -b<pos1_start_column> -e<pos1_end_column> [-u<pos2_start_column> -v<pos2_end_column>] [-T] textfile.gz    # u, v is required for full 2d query.
```

Exemplo para realizar query:

```bash
pairix textfile.gz region1 [region2 [...]]  ## region is in the following format.

# for 1D indexed file
pairix textfile.gz '<chr>:<start>-<end>' '<chr>:<start>-<end>' ...

# for 2D indexed file
pairix [-a] textfile.gz '<chr1>:<start1>-<end1>|<chr2>:<start2>-<end2>' ...    # make sure to quote so '|' is not interpreted as a pipe.
pairix [-a] textfile.gz '*|<chr2>:<start2>-<end2>'  # wild card is accepted for 1D query on 2D indexed file
pairix [-a] textfile.gz '<chr1>:<start1>-<end1>|*' # wild card is accepted for 1D query on 2D indexed file
```

Consulte sobre a utilização, opções e  parâmetros disponíveis com `pairix -h` e informações mais detalhadas na [no repositório do pairix](https://github.com/4dn-dcic/pairix/blob/master/README.md).

## Submetendo jobs

A execução do pairix no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `pairix.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=pairix
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=2
#SBATCH --mem-per-cpu=2GB

module load pairix/0.3.9

INPUT_PAIRS="pairs_file.gz"
REGION_1="<chr>:<start>-<end>"
REGION_2="<chr>:<start>-<end>"

pairix "$INPUT_PAIRS" "$REGION_1" "$REGION_2"
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch pairix.sh
```

Para mais detalhes sobre os parâmetros do pairix, use:

```bash
pairix -h
```
