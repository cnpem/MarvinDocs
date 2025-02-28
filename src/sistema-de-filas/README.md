# Sistema de Filas 📋

Em ambientes HPC, múltiplos usuários podem estar logados simultaneamente. Na tentativa de atender a necessidade de todos são utilizados programas que gerenciam a alocação de recursos (cpus, memória, etc) e a ordem de execução das tarefas. No Marvin utilizamos o [SLURM](https://slurm.schedmd.com/overview.html).

Parte dessa organização ocorre por meio de **filas** de execução, chamadas de _partitions_ no **SLURM**. Essas filas guardam as tarefas que os usuários submetem e, assim que houver recurso disponíveis, iniciam a sua execução.

## As filas do Marvin

No Marvin temos filas específicas de acordo com o recurso desejado pelo usuário: apenas CPU, CPU+GPU(5GB) ou CPU+GPU(40GB). Também dividimos pelo tempo de execução que o usuário deseja reservar para a tarefa: até 30 min, 12 horas, 5 dias e 15 dias.

Assim as filas são:

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

## Políticas de filas

Até o momento, nossa opção tem sido estimular boas práticas ao invés de estabelecer regras mais restritivas.

Abaixo estão algumas dicas em relação a escolha e uso das filas:

- Cada fila tem uma quantidade de recursos reservados por padrão (_default_). Normalmente os valores são bem inferiores ao limite máximo de recursos que fila permite reservar por tarefa. Tente escolher sempre a fila capaz de fornecer os recursos necessário para atender a execução da sua tarefa, faça os ajustes e evite deperdícios!  
- Se a tarefa não utiliza a GPU o usuário deve preferir as filas **cpu** como `short-cpu` e `long-cpu`.
- Se o usuário deseja identificar um erro que está ocorrendo em uma tarefa (_debugar_) é preferível que sejam utilizadas as filas de **debug** como `debug-cpu`, `debug-gpu-small` e `debug-gpu-big`.
- Tarefas executadas de forma interativas, o que é mais comum quando se utiliza interface gráfica como VNC, RStudio e Jupyter, são menos eficientes no uso de recurso computacionais, mas podem ser úteis para análises rápidas de resultados e preparação de tarefas. Por esses motivos foram criadas as filas **gui** (_Graphical User Interface_). Intencionalmente elas tem tempo limite de 12 horas para que os usuários não esqueçam tarefas ativas e ociosas de um dia para o outro.
- O usuário deve evitar submeter muitos jobs simultaneamente a fim de evitar uma monopolização das filas por um longo período.
- Nas filas **short-cpu** e **short-gpu** é possível alocar, respectivamente, até 4GB e 8GB de memória RAM **por cpu** (parâmetro _mem-per-cpu_ do SLURM), mas por padrão são alocados 1GB por cpu. Ajuste esse parâmetro e o número de cpus da tarefa antes de pensar em utilizar as filas **bigmen** e **highmem**.
- Ainda sobre as filas **bigmen** e **highmem**, elas são para **casos excepcionais**, pois reservam uma quantidade enorme de memória por cpu, até 132GB, o que pode impactar outros usuários.  
