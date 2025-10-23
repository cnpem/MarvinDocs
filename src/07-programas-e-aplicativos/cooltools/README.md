# cooltools

O [cooltools](https://github.com/open2c/cooltools/) é uma biblioteca Python voltada para a análise avançada de dados Hi-C. Ela se integra diretamente com arquivos `.cool`, oferecendo funções para calcular métricas de interação cromossômica, como isolamento de domínios TAD, correlações de compartimentos, métricas de cis/trans e muito mais. O cooltools combina utilitários de linha de comando e funções Python, permitindo análises flexíveis e reprodutíveis em diferentes resoluções de dados Hi-C.  

Para mais informações e documentação completa, acesse: <https://cooltools.readthedocs.io/en/latest/>

## Carregando o módulo

Para habilitar o cooltools no HPCC Marvin, você deve carregar o módulo `cooltools`:

```bash
module load cooltools
```

<div class="warning">
    <br>As versões disponíveis do cooltools no HPCC Marvin são:
    <ul>
        <li><code>cooltools/0.7.1   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help cooltools
```

## Executando o módulo

Modelo de uso do cooltools via linha de comando:

```bash
cooltools [OPTIONS] COMMAND [ARGS]...
```

Ao executar `cooltools -h`, é possível consultar a lista de comandos disponíveis:

```text
Commands:
  coverage        Calculate the sums of cis and genome-wide contacts (aka...
  dots            Call dots on a Hi-C heatmap that are not larger than...
  eigs-cis        Perform eigen value decomposition on a cooler matrix to...
  eigs-trans      Perform eigen value decomposition on a cooler matrix to...
  expected-cis    Calculate expected Hi-C signal for cis regions of...
  expected-trans  Calculate expected Hi-C signal for trans regions of...
  genome          Utilities for binned genome assemblies.
  insulation      Calculate the diamond insulation scores and call...
  pileup          Perform retrieval of the snippets from .cool file.
  random-sample   Pick a random sample of contacts from a Hi-C map.
  rearrange       Rearrange data from a cooler according to a new genomic...
  saddle          Calculate saddle statistics and generate saddle plots...
  virtual4c       Generate virtual 4C profile from a contact map by...
```

Consulte todos informações completas sobre os comandos na página de [referência de CLI na documentação oficial do cooltools](https://cooltools.readthedocs.io/en/latest/cli.html).

## Submetendo jobs

A execução do cooltools no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `cooltools.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=cooltools
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem-per-cpu=4GB

module load cooltools/0.7.1

COOL_PATH="/caminho/para/arquivo.cool"
OUTPUT="/caminho/para/output.tsv"

cooltools coverage -o  "$OUTPUT" "$COOL_PATH"
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch cooltools.sh
```

Para mais detalhes sobre os parâmetros de cada comando do cooltools, use:

```bash
cooltools [COMMAND] -h
```
