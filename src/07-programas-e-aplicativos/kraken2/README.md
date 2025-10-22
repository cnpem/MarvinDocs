# Kraken2

O [Kraken2](https://github.com/DerrickWood/kraken2/) é uma ferramenta de **classificação taxonômica ultrarrápida para dados de sequenciamento metagenômico**, baseada na correspondência exata de *k*-mers.  

Ele permite identificar rapidamente a **composição taxonômica de amostras biológicas** a partir de leituras de DNA, atribuindo cada sequência ao nível taxonômico mais específico possível.  

O Kraken2 é amplamente utilizado em estudos de **microbiomas, viromas e análises ambientais**, oferecendo alto desempenho e precisão por meio de **índices otimizados e bases de dados personalizáveis**.  

Para mais informações, acesse: <https://github.com/DerrickWood/kraken2/>

## Carregando o módulo

Para habilitar o kraken2 no HPCC Marvin, você deve carregar o módulo `kraken2`:

```bash
module load kraken2
```

<div class="warning">
    <br>As versões disponíveis do kraken2 no HPCC Marvin são:
    <ul>
        <li><code>kraken2/2.1.6   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help kraken2
```

## Executando o módulo

Na segunda versão do kraken, é possível executá-lo via um wrapper script com o binário `k2` em combinação com alguns comandos como `add-to-library` e `build`. O `k2` oferece suporte a todas as opções de linha de comando dos scripts originais e adiciona alguns novos recursos que estão documentados no manual.

Por exemplo, para verificar obter o help do comando `build`, execute:

```bash
k2 build -h
```

Consulte todos os comandos disponíveis com `k2 -h` e documentação mais detalhada no [manual do Kraken2 no GitHub](https://github.com/4dn-dcic/kraken2/).

## Submetendo jobs

A execução do kraken2 no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `kraken2.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=kraken2
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem-per-cpu=4GB

module load kraken2/2.1.6

DB_PATH="/caminho/para/kraken.db"

k2 build --db "$DB_PATH"
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch kraken2.sh
```

Para mais detalhes sobre os parâmetros do kraken2, use:

```bash
k2 -h
```
