# SLURM Básico para Iniciantes

O SLURM (Simple Linux Utility for Resource Management) é o sistema de gerenciamento de filas usado no cluster HPC Marvin. Este guia foi desenvolvido para ajudar usuários iniciantes a entender e utilizar os comandos básicos do SLURM.

## O que é o SLURM?

O SLURM é um sistema de gerenciamento de filas de código aberto projetado para organizar o acesso aos recursos computacionais em um cluster. Ele permite que múltiplos usuários compartilhem os recursos do cluster de forma eficiente.

## Comandos Básicos do SLURM

### Submeter um Trabalho

Para submeter um trabalho, use o comando `sbatch` seguido do nome do script:

```bash
sbatch meu_script.sh
```

### Exemplo de Script Básico

Aqui está um exemplo simples de um script de submissão:

```bash
#!/bin/bash
#SBATCH --job-name=teste       # Nome do trabalho
#SBATCH --partition=debug-cpu  # Nome do trabalho
#SBATCH --nodes=1              # Solicita 1 nó
#SBATCH --ntasks=1             # Solicita 1 tarefa
#SBATCH --cpus-per-task=1      # Solicita 1 CPU por tarefa
#SBATCH --mem=1G               # Solicita 1GB de memória RAM
#SBATCH --time=00:10:00        # Tempo máximo de execução: 1 hora
#SBATCH --output=output_%j.log # Arquivo de saída (%j é substituído pelo ID do job)

# Comandos a serem executados
echo "Olá do cluster Marvin!"
hostname
date
sleep 60  # Aguarda 60 segundos
echo "Trabalho concluído."
```

### Verificar Status dos Trabalhos

Para ver o status de todos os seus trabalhos:

```bash
squeue -u $USER
```

Para ver detalhes de um trabalho específico:

```bash
scontrol show job 123456  # Substitua 123456 pelo ID do seu trabalho
```

### Cancelar um Trabalho

Para cancelar um trabalho específico:

```bash
scancel 123456  # Substitua 123456 pelo ID do trabalho
```

Para cancelar todos os seus trabalhos:

```bash
scancel -u $USER
```

## Recursos Adicionais

### Solicitando Recursos Específicos

Para solicitar GPUs:

```bash
#SBATCH --gres=gpu:1  # Solicita 1 GPU
```

Para especificar uma partição:

```bash
#SBATCH --partition=short-gpu-small  # Submete para a partição "gpu"

```

### Trabalhos Interativos

Para iniciar uma sessão interativa:

```bash
srun --pty bash -i
```

Ou com recursos específicos:

```bash
srun --pty --nodes=1 --ntasks=1 --cpus-per-task=4 --mem=8G --time=02:00:00 bash -i
```

### Verificando Recursos Disponíveis

Para ver as partições disponíveis e seus limites:

```bash
sinfo
```

Para ver informações detalhadas sobre os nós:

```bash
sinfo -N -l
```

## Dicas Úteis

1. **Sempre especifique os recursos necessários**: Isso ajuda o SLURM a agendar seu trabalho de forma mais eficiente.
2. **Defina o tempo limite adequado**: Muito curto pode interromper seu trabalho; muito longo pode atrasar o agendamento.
3. **Use o arquivo de saída**: Verifique os arquivos de saída para depurar problemas ou confirmar resultados.
4. **Teste com trabalhos pequenos**: Antes de submeter trabalhos grandes, teste com versões menores para garantir que tudo está funcionando corretamente.

## Glossário Rápido

- **Job/Trabalho**: Uma unidade de trabalho enviada ao SLURM para execução.
- **Node/Nó**: Um computador físico no cluster.
- **Task/Tarefa**: Um processo em execução, geralmente corresponde a um processo MPI.
- **Partition/Partição**: Um conjunto de nós com limitações e configurações específicas.
- **GRES (Generic RESource)**: Recursos genéricos como GPUs.

Para informações mais detalhadas, consulte a [documentação oficial do SLURM](https://slurm.schedmd.com/) ou entre em contato com a equipe de suporte do Marvin.
