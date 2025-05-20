# Sistema de filas

Em ambientes HPC, é comum que múltiplos usuários estejam logados e executando _jobs_ simultaneamente. Para gerenciar eficientemente a alocação de recursos (CPU, GPU, memória, etc)
e a ordem de execução desses _jobs_, são usados sistemas de gerenciamento de filas.

O gerenciador de filas usado éo [SLURM](https://slurm.schedmd.com/overview.html) v21.08.8-2, que organiza a execução por meio de filas, chamadas de _partitions_, que armazenam os _jobs_ submetidos pelos usuários. Assim que os recursos solicitados estão disponíveis, o SLURM inicia a execução dessas tarefas de forma automática.

<div class="warning"> 
Todos os <i>jobs</i> devem ser submetidos através do SLURM.
</div>

As filas de execução do HPCC Marvin são:

| Fila             | Tempo limite | cpus-per-task (limite) | mem-per-cpu (default) | mem-per-cpu (limite) | GPU         |
|------------------|:------------:|:----------------------:|:---------------------:|:--------------------:|:-----------:|
| debug-cpu        | 30 minutos   |           2            |          1GB          |         2GB          |     Não     |
| gui-cpu          | 12 horas     |           8            |          1GB          |         4GB          |     Não     |
| short-cpu        | 5 dias       |           64           |          1GB          |         4GB          |     Não     |
| long-cpu         | 15 dias      |           32           |          1GB          |         4GB          |     Não     |
| debug-gpu-small  | 30 minutos   |           2            |          1GB          |         2GB          |   Sim (5GB) |
| gui-gpu-small    | 12 horas     |           8            |          1GB          |         4GB          |   Sim (5GB) |
| short-gpu-small  | 5 dias       |           64           |          1GB          |         8GB          |   Sim (5GB) |
| long-gpu-small   | 15 dias      |           32           |          1GB          |         8GB          |   Sim (5GB) |
| debug-gpu-big    | 30 minutos   |           2            |          1GB          |         2GB          |  Sim (40GB) |
| gui-gpu-big      | 12 horas     |           8            |          1GB          |         4GB          |  Sim (40GB) |
| short-gpu-big    | 5 dias       |           64           |          1GB          |         8GB          |  Sim (40GB) |
| long-gpu-big     | 15 dias      |           32           |          1GB          |         8GB          |  Sim (40GB) |

## Boas práticas no uso das filas

O Marvin adota uma política de incentivo às boas práticas, ao invés de aplicar restrições rígidas. A seguir, destacamos algumas recomendações importantes:

- **Escolha consciente da fila:** cada fila possui um valor padrão (_default_) e um limite máximo de recursos por tarefa. Escolha a fila que oferece os recursos necessários para sua tarefa e ajuste os parâmetros para evitar desperdícios.

- **Uso adequado das filas CPU:** se a tarefa não requer GPU, prefira as filas exclusivamente CPU, como `short-cpu` e `long-cpu`.

- **Depuração de códigos:** para identificar erros em tarefas, utilize preferencialmente as filas de depuração (`debug-cpu`, `debug-gpu-small`, `debug-gpu-big`), que oferecem retorno rápido.

- **Filas GUI:** filas como `gui-cpu` e `gui-gpu-*` são destinadas ao uso com interfaces gráficas (VNC, RStudio, Jupyter). São menos eficientes para execução contínua, mas úteis para testes rápidos ou preparação de análises. Seu tempo máximo é limitado a 12 horas para evitar processos esquecidos em execução.

- **Evite saturar as filas:** não submeta muitos _jobs_ simultaneamente, para não monopolizar recursos e impactar negativamente outros usuários.

- **Ajuste de memória:** em filas como `short-cpu` e `short-gpu-*`, é possível alocar até 4 GB ou 8 GB de RAM por CPU, respectivamente, utilizando o parâmetro `--mem-per-cpu` no SLURM. O padrão é 1 GB por CPU, portanto, ajuste este valor quando necessário antes de migrar para filas com mais memória.

- **Uso das filas de alta memória:** filas como `bigmem` ou `highmem` (quando disponíveis) devem ser usadas apenas em casos excepcionais, pois alocam até 132 GB de RAM por CPU e podem prejudicar a disponibilidade de recursos para outros usuários.

