# Submissão de _jobs_

Para submeter um _job_, você deve criar um script de submissão com os parâmetros adequados e usar o comando `sbatch`:

```bash
sbatch teste.sh
```

O script de submissão define as características do trabalho, como nome, partição, número de nós e CPUs, memória, tempo máximo de execução, e arquivos de saída. Um exemplo básico:

```bash
#!/bin/bash
#SBATCH --job-name=teste
#SBATCH --partition=debug-cpu
#SBATCH --cpus-per-task=1
#SBATCH --mem=1G
#SBATCH --time=00:10:00
#SBATCH --output=output_%j.log

echo "Olá do cluster Marvin!"
hostname
date
sleep 60
echo "Trabalho concluído."
```

## Indicando a partição do SLURM (fila)

Para especificar uma partição (fila) use:

```bash
#SBATCH --partition=<substitua pelo nome da partição>
```

Cada partição ou fila possui recursos e limites diferentes, elas podem ser consultadas em [Sistema de filas](../03-arquitetura/sistema-de-filas).


## Solicitando recursos específicos

* Solicite o número de CPUs para a tarefa

```bash
#SBATCH --cpus-per-task=<substitua pelo numero de cpus>
```

* A solicitação de GPUs varia de acordo com a partição. Partições `*-gpu-small` possuem GPUs de 5GB de memória, enquanto que partições `*-gpu-big` possuem GPUs A100 com 40GB de memória.

Para as filas `*-gpu-small` use:
```bash
#SBATCH --gres=gpu:1g.5gb:1 
```

Para as filas `*-gpu-big` use:
```bash
#SBATCH --gres=gpu:a100:1 
```

* A solicitação da quantidade de memória pode ser feita em quantidade total para o job ou quantidade por cpu.

Para solicitar a quantidade total use:

```bash
#SBATCH --mem=16G 
```

Para solicitar a quantidade por CPU use:

```bash
#SBATCH --mem-per-cpu=4GB
```

* Solicitação de tempo

Para um melhor funcionamento do sistema gerenciador de tarefas e recursos (SLURM) __é importante__ que o usuário indique o tempo aproximado de execução da tarefa, mesmo sendo sobreestimado. Através desse tempo, o SLURM conseguirá alocar jobs em janelas ociosas e otimizar o uso dos recursos. 

Exemplo solicitando 10 horas de tempo de processamento.

```bash
#SBATCH --time=10:00:00 
```


## Trabalhos interativos

Você pode iniciar uma sessão interativa com:

```bash
srun -p debug-cpu --pty bash 
```

Ou com recursos definidos:

```bash
srun -p short-gpu-small --gres gpu:1g.5gb:1 -c 4 --mem 8G --time 01:00:00 --pty bash 
```
