# Arquitetura e Sistema de Filas

Neste capítulo, apresentaremos uma visão geral da arquitetura do HPC Marvin e do
sistema de filas que gerencia as solicitações de processamento dos usuários.

## Arquitetura do HPC Marvin 💻

Nesta seção, descreveremos a arquitetura geral do HPC Marvin, incluindo
informações sobre o hardware utilizado, o sistema operacional e o software
instalado.

### Hardware

Nesta seção, apresentaremos a infraestrutura de hardware utilizada no HPC
Marvin, incluindo informações sobre os processadores, memória RAM, armazenamento
em disco, entre outros.

O HPC Marvin é composto por um cluster de servidores interconectados dedicados
ao processamento intensivo e armazenamento de dados. O cluster é composto pelos
seguintes componentes:

- `01` servidor de login;
- `01` servidor de processamento em CPU e 1TB de memória RAM;
- `01` servidor de processamento em GPU equipado com 8 NVIDIA A100 40GB e 2TB de memória RAM;
- Sistema de armazenamento de dados (_storage_) Lustre contendo:
  - `06` servidores com SSD/NVMe, totalizando 300TB de espaço disponível.

Com essa infraestrutura de hardware, o HPC Marvin é capaz de oferecer um
ambiente de processamento robusto e eficiente para as necessidades
computacionais dos usuários.

### Sistema Operacional

Nesta seção, descreveremos o sistema operacional utilizado no HPC Marvin,
incluindo sua versão e principais recursos.

### Programas e Aplicativos

Aqui, forneceremos uma lista dos principais softwares instalados no HPC Marvin,
como compiladores, bibliotecas e ferramentas de programação.

## Sistema de Filas 📋

Em ambientes HPC, múltiplos usuários podem estar logados simultaneamente. Na tentativa de atender a necessidade de todos são utilizados programas que gerenciam a alocação de recursos (cpus, memória, etc) e a ordem de execução das tarefas. No Marvin utilizamos o [SLURM](https://slurm.schedmd.com/overview.html).

Parte dessa organização ocorre por meio de **filas** de execução, chamadas de _partitions_ no SLURM. Essas filas guardam as tarefas que os usuários submetem e, assim que houver recurso disponíveis, iniciam a sua execução. 

### Tipos de filas

<!-- Aqui, apresentaremos os diferentes tipos de filas disponíveis no HPC Marvin, -->
<!-- incluindo filas para processamento de longa duração, filas para processamento de -->
<!-- curta duração, dentre outras. -->

No Marvin temos filas específicas de acordo com o recurso desejado pelo usuário: apenas CPU, CPU+GPU(5GB) ou CPU+GPU(40GB). Também dividimos pelo tempo de execução que o usuário deseja reservar para a tarefa: até 15 min, 12 horas, 5 dias e 15 dias. 

Assim as filas são:

| Fila            | tempo limite |   |   |   |
|-----------------|--------------|---|---|---|
| short-cpu       | 5 dias       |   |   |   |
| long-cpu        | 15 dias      |   |   |   |
| short-gpu-small | 5 dias       |   |   |   |
| long-gpu-small  | 15 dias      |   |   |   |
|                 |              |   |   |   |
|                 |              |   |   |   |

### Políticas de filas

Nesta seção, descreveremos as políticas de filas utilizadas no HPC Marvin para
determinar a ordem em que as solicitações são processadas, incluindo a política
de prioridade e a política de justiça.

### Submissão de trabalhos

Aqui, explicaremos como os usuários podem submeter seus trabalhos para o sistema
de filas do HPC Marvin, incluindo as opções de configuração disponíveis.

### Monitoramento de trabalhos

Nesta seção, descreveremos como os usuários podem monitorar o status de seus
trabalhos, incluindo informações sobre o tempo de execução e a utilização dos
recursos do sistema.
