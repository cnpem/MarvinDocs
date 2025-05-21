## Instalação do OMERO.Insight

Neste capítulo, você encontrará todas as informações necessárias para submeter seus trabalhos ao cluster Sonny. Serão abordados diferentes tipos de trabalhos, como submeter, monitorar e gerenciar esses trabalhos em execução.

## Upload de dados do Operetta

O SLURM suporta vários tipos de trabalhos que podem ser submetidos ao cluster. Abaixo estão alguns dos tipos de trabalhos mais comuns:

- Batch jobs: Trabalhos que são executados em lotes, geralmente sem intervenção humana e com um tempo de execução limitado. Esses trabalhos são adequados para tarefas que podem ser executadas em lotes sem a necessidade de interação humana, como processamento de dados em larga escala.

- CPU jobs: Trabalhos de matriz são um conjunto de tarefas semelhantes que são executadas em paralelo em várias CPUs ou nós. Esses trabalhos são adequados para tarefas que podem ser divididas em tarefas menores e executadas em paralelo, como simulações ou processamento de imagens.

- GPU jobs: Trabalhos que utilizam aceleração de GPU para melhorar o desempenho de tarefas intensivas em computação. Esses trabalhos são adequados para tarefas que exigem muito poder de processamento, como modelagem de clima ou treinamento de modelos de aprendizado de máquina.

- MPI jobs: Trabalhos que utilizam bibliotecas MPI (Message Passing Interface) para permitir a comunicação entre diferentes nós do cluster. Esses trabalhos são adequados para tarefas que exigem comunicação entre nós do cluster, como simulações em escala molecular ou simulações de dinâmica de fluidos computacional.

Cada tipo de trabalho tem seus próprios requisitos de submissão e comandos associados. É importante escolher o tipo de trabalho mais adequado para sua tarefa e garantir que as opções de submissão estejam corretas para evitar problemas durante a execução.

## Upload de dados do Cytation

O SLURM é um sistema de gerenciamento de trabalhos que permite aos usuários submeter trabalhos para execução no cluster Sonny. Nesta seção, você encontrará informações detalhadas sobre como submeter trabalhos usando o SLURM.

- Preparar o script de submissão de trabalho:

Para submeter um trabalho com o SLURM, você precisa criar um script que contenha as informações sobre o trabalho a ser executado, como o nome do trabalho, quantidade de CPUs, quantidade de memória, tempo de execução, diretório de trabalho e arquivos de entrada e saída. O script deve ser salvo com a extensão `.sh`.

Um exemplo de script de submissão de trabalho com SLURM é mostrado abaixo:

```bash
#!/bin/bash
#SBATCH --job-name=teste       # nome do trabalho
#SBATCH --output=teste.out     # arquivo de saída
#SBATCH --error=teste.err      # arquivo de erro
#SBATCH --ntasks=1             # número de tarefas
#SBATCH --cpus-per-task=4      # número de CPUs por tarefa
#SBATCH --mem-per-cpu=2000     # quantidade de memória por CPU
#SBATCH --time=01:00:00        # tempo máximo de execução
#SBATCH --workdir=/caminho/para/diretorio/de/trabalho

srun python meu_programa.py   # comando para executar o programa
```

No exemplo acima, o script teste.sh é criado com o nome do trabalho, os arquivos de saída e erro, a quantidade de tarefas, CPUs e memória por CPU, tempo máximo de execução e diretório de trabalho especificados. O comando srun é usado para executar o programa `meu_programa.py`.

- Submeter o script de submissão de trabalho:

Após criar o script de submissão de trabalho com Slurm, você precisa enviar o script para o cluster Sonny usando o comando `sbatch`. O comando `sbatch` é usado para submeter trabalhos ao sistema de gerenciamento de trabalhos.

Por exemplo, para enviar o script `teste.sh` para o cluster Sonny, execute o seguinte comando:

```bash
sbatch teste.sh
```

- Exemplos de scripts de submissão de trabalho:

Nesta seção, você encontrará alguns exemplos de scripts para submeter seus trabalhos ao cluster Sonny. Os exemplos abordados são:

1. Trabalho utilizando CPU:

```bash
#!/bin/bash
#SBATCH --job-name=teste_cpu
#SBATCH --output=teste_cpu.out
#SBATCH --error=teste_cpu.err
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem-per-cpu=2000
#SBATCH --time=01:00:00
#SBATCH --workdir=/caminho/para/diretorio/de/trabalho

srun python meu_programa_cpu.py
```

2. Trabalho utilizando GPU:

```bash
#!/bin/bash
#SBATCH --job-name=teste_gpu
#SBATCH --output=teste_gpu.out
#SBATCH --error=teste_gpu.err
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --mem-per-cpu=2000
#SBATCH --time=01:00:00
#SBATCH --partition=gpu # indica que o job utilizará GPUs
#SBATCH --gres=gpu:1 # indica a quantidade de GPUs a serem utilizadas
#SBATCH --nodelist=node1 # nome do nó a ser utilizado (caso o cluster possua mais de um)

srun python meu_programa_gpu.py
```

3. Trabalho utilizando MPI:

```bash
#!/bin/bash
#SBATCH --job-name=teste_mpi
#SBATCH --output=teste_mpi.out
#SBATCH --error=teste_mpi.err
#SBATCH --ntasks=8
#SBATCH --ntasks-per-node=2
#SBATCH --mem-per-cpu=2000
#SBATCH --time=01:00:00
#SBATCH --workdir=/caminho/para/diretorio/de/trabalho

mpirun -np 8 meu_programa_mpi.py
```

Estes são apenas alguns exemplos básicos, e é importante lembrar que cada trabalho pode ter requisitos e opções específicas de acordo com a tarefa e o cluster utilizado. Portanto, é sempre recomendável verificar a documentação do sistema de gerenciamento de trabalhos e as especificações do cluster antes de criar um script de submissão de trabalho.

## Monitoramento de Trabalhos em Execução

O monitoramento de trabalhos em execução em um cluster é uma tarefa essencial para garantir a eficiência e a produtividade do sistema. Nesta seção, você encontrará informações sobre como realizar essa tarefa no cluster Sonny, por meio do uso dos comandos `squeue`, `sinfo` e `scontrol`.

- Status dos trabalhos em execução:

O comando `squeue` é usado para verificar o status dos trabalhos em execução. Com ele, você pode visualizar informações como o ID do trabalho, o usuário que o submeteu, o estado em que se encontra e o tempo que está em execução.

```bash
marie.currie@sonny:~> squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
              8690 compute*  sys/dash albert.e  R    1:19:05      1 gpu01
              8657 compute*      1605 albert.e  R   23:43:34      1 gpu01
              8717 compute*     40366 stephen.  R       6:48      1 gpu01
              8656 compute*      6160 stephen.  R   23:44:17      1 gpu01
              8664 compute*      6235 stephen.  R    7:42:11      1 gpu01
              8683 compute*      6033 carl.sag  R    2:24:20      1 gpu01
              8660 compute*  sys/dash carl.sag  R    8:21:11      1 gpu01
              8662 compute*      5714 carl.sag  R    8:02:30      1 gpu01
```

- Informações sobre a carga do sistema:

O comando `sinfo` é utilizado para visualizar informações sobre a carga do sistema. Com ele, você pode verificar o número de nós disponíveis, sua capacidade de processamento, a carga atual e outras informações importantes para o planejamento de novos trabalhos.

```bash
marie.currie@sonny:~> sinfo
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
compute*     up 5-00:00:00      1   idle gpu01
```

- Tempo de espera dos trabalhos

O comando `scontrol show job <JOBID>` é usado para determinar o tempo de espera dos trabalhos. Com ele, você pode verificar informações sobre o tempo que o trabalho está em espera, o tempo de execução previsto e outros detalhes que podem ajudar a melhorar a eficiência do sistema.

```bash
marie.currie@sonny:~> scontrol show job 8690
JobId=8690 JobName=sys/dashboard/sys/bc_desktop/desktop
   UserId=albert.einstein(1250890533) GroupId=domain users(1250800513) MCS_label=N/A
   Priority=4294895570 Nice=0 Account=root QOS=normal
   JobState=RUNNING Reason=None Dependency=(null)
   Requeue=1 Restarts=0 BatchFlag=1 Reboot=0 ExitCode=0:0
   RunTime=01:26:30 TimeLimit=02:00:00 TimeMin=N/A
   SubmitTime=2023-04-13T14:28:21 EligibleTime=2023-04-13T14:28:21
   AccrueTime=2023-04-13T14:28:21
   StartTime=2023-04-13T14:28:21 EndTime=2023-04-13T16:28:21 Deadline=N/A
   SuspendTime=None SecsPreSuspend=0 LastSchedEval=2023-04-13T14:28:21 Scheduler=Main
   Partition=gui-gpu-small AllocNode:Sid=marvin:840269
   ReqNodeList=(null) ExcNodeList=(null)
   NodeList=gpu01
   BatchHost=gpu01
   NumNodes=1 NumCPUs=2 NumTasks=1 CPUs/Task=1 ReqB:S:C:T=0:0:*:*
   TRES=cpu=2,mem=4G,node=1,billing=2,gres/gpu=1,gres/gpu:a100=1
   Socks/Node=* NtasksPerN:B:S:C=0:0:*:1 CoreSpec=*
   MinCPUsNode=1 MinMemoryNode=0 MinTmpDiskNode=0
   Features=(null) DelayBoot=00:00:00
   OverSubscribe=OK Contiguous=0 Licenses=(null) Network=(null)
   Command=(null)
   WorkDir=/home/albert.einstein/ondemand/data/sys/dashboard/batch_connect/sys/bc_desktop/desktop/output/5701565f-5c7c-4c94-b237-ced38c8248c3
   StdErr=/home/albert.einstein/ondemand/data/sys/dashboard/batch_connect/sys/bc_desktop/desktop/output/5701565f-5c7c-4c94-b237-ced38c8248c3/output.log
   StdIn=/dev/null
   StdOut=/home/albert.einstein/ondemand/data/sys/dashboard/batch_connect/sys/bc_desktop/desktop/output/5701565f-5c7c-4c94-b237-ced38c8248c3/output.log
   Power=
   MemPerTres=gpu:4096
   TresPerJob=gres:gpu:1

```

## Gerenciamento de Trabalhos

Nesta seção, você encontrará informações sobre como gerenciar os trabalhos no cluster Sonny.

- Cancelar um trabalho:

O comando `scancel <JOBID>` é usado para cancelar um trabalho pelo ID (JOBID) que está sendo executado no cluster.

```bash
scancel <JOBID>
```

Para mais informações sobre o SLURM, acesse sua documentação: <https://slurm.schedmd.com/documentation.html>.
