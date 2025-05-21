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
#SBATCH --nodes=1
#SBATCH --ntasks=1
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

### Solicitando recursos específicos

* Para solicitar GPUs:

```bash
#SBATCH --gres=gpu:1
```

* Para especificar uma partição (fila):

```bash
#SBATCH --partition=short-gpu-small
```

### Trabalhos interativos

Você pode iniciar uma sessão interativa com:

```bash
srun --pty bash -i
```

Ou com recursos definidos:

```bash
srun --partition=short-gpu-small --gres=gpu:1 --cpus-per-task=4 --mem=8G --time=01:00:00 --pty bash -i
```
