# pairtools

O [pairtools](https://github.com/open2c/pairtools/) é um conjunto de ferramentas em linha de comando e biblioteca Python desenvolvido para processar e manipular dados de pares de leituras provenientes de experimentos Hi-C. Ele realiza etapas essenciais do pipeline, como emparelhamento de leituras mapeadas, filtragem, deduplicação e indexação, gerando arquivos `.pairs` padronizados que descrevem interações cromossômicas individuais. O pairtools é altamente eficiente e modular, podendo ser integrado a pipelines maiores para análise de dados genômicos em larga escala.  

Para mais informações e documentação completa, acesse: <https://pairtools.readthedocs.io/en/latest/index.html>

## Carregando o módulo

Para habilitar o pairtools no HPCC Marvin, você deve carregar o módulo `pairtools`:

```bash
module load pairtools
```

<div class="warning">
    <br>As versões disponíveis do pairtools no HPCC Marvin são:
    <ul>
        <li><code>pairtools/1.1.3   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help pairtools
```

## Executando o módulo

Modelo de uso do pairtools via linha de comando:

```bash
pairtools [OPTIONS] COMMAND [ARGS]...
```

Ao executar `pairtools -h`, é possível consultar a lista de comandos disponíveis:

```text
Commands:
  dedup        Find and remove PCR/optical duplicates.
  filterbycov  Remove pairs from regions of high coverage.
  flip         Flip pairs to get an upper-triangular matrix.
  header       Manipulate the .pairs/.pairsam header
  markasdup    Tag all pairs in the input file as duplicates.
  merge        Merge .pairs/.pairsam files.
  parse        Find ligation pairs in .sam data, make .pairs.
  parse2       Extracts pairs from .sam/.bam data with complex walks,...
  phase        Phase pairs mapped to a diploid genome.
  restrict     Assign restriction fragments to pairs.
  sample       Select a random subset of pairs in a pairs file.
  scaling      Calculate pairs scalings.
  select       Select pairs according to some condition.
  sort         Sort a .pairs/.pairsam file.
  split        Split a .pairsam file into .pairs and .sam.
  stats        Calculate pairs statistics.
```

Consulte todos informações completas sobre os comandos na página de [referência de CLI na documentação oficial do pairtools](https://pairtools.readthedocs.io/en/latest/cli_tools.html).

## Submetendo jobs

A execução do pairtools no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `pairtools.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=pairtools
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem-per-cpu=4GB

module load pairtools/1.1.3

PAIRS_PATH="/caminho/para/arquivo.pairs"
OUTPUT="/caminho/para/output.tsv"

pairtools dedup -o  "$OUTPUT" "$PAIRS_PATH"
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch pairtools.sh
```

Para mais detalhes sobre os parâmetros de cada comando do pairtools, use:

```bash
pairtools [COMMAND] -h
```
