# O que é um _job_?

Um job é uma tarefa computacional submetida para execução no cluster, como scripts, programas, simulações ou qualquer outro tipo de processamento.

No HPCC Marvin, os jobs são enviados ao SLURM por meio de scripts de submissão. O SLURM insere os jobs em uma fila e os executa conforme a disponibilidade dos recursos, seguindo políticas de agendamento definidas.

Cada job pode variar em complexidade: desde a execução de um único comando até fluxos compostos por múltiplas etapas e dependências. Os usuários podem especificar requisitos como número de CPUs, quantidade de memória, uso de GPUs e tempo estimado de execução.

Os jobs podem ser executados em segundo plano (`sbatch`) ou de forma interativa (`srun --pty bash -i`), conforme a necessidade. O SLURM também oferece recursos avançados, como monitoramento em tempo real, controle de dependências e suporte à retomada em caso de falhas.
