# Sistema de filas

Em ambientes HPC, é comum que múltiplos usuários estejam logados e executando _jobs_ simultaneamente. Para gerenciar eficientemente a alocação de recursos (CPU, GPU, memória, etc)
e a ordem de execução desses _jobs_, são usados sistemas de gerenciamento de filas.

O gerenciador de filas usado é o [SLURM](https://slurm.schedmd.com/overview.html) v21.08.8-2, que organiza a execução por meio de filas, chamadas de _partitions_, que armazenam os _jobs_ submetidos pelos usuários. Assim que os recursos solicitados estão disponíveis, o SLURM inicia a execução dessas tarefas de forma automática.

<div class="warning">
    <br>Todos os <i>jobs</i> devem ser submetidos através do SLURM.<br>
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
