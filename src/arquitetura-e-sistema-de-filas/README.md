# Arquitetura e Sistema de Filas

Neste capítulo, apresentaremos uma visão geral da arquitetura do HPC Marvin e do sistema de filas que gerencia as solicitações de processamento dos usuários.

## Arquitetura do HPC Marvin 💻

Nesta seção, descreveremos a arquitetura geral do HPC Marvin, incluindo informações sobre o hardware utilizado, o sistema operacional e o software instalado.

### Hardware

Nesta seção, apresentaremos a infraestrutura de hardware utilizada no HPC Marvin, incluindo informações sobre os processadores, memória RAM, armazenamento em disco, entre outros.

O HPC Marvin é composto por um cluster de servidores interconectados dedicados ao processamento intensivo e armazenamento de dados. O cluster é composto pelos seguintes componentes:

- Um servidor de login;
- Um servidor de processamento em CPU;
- Um servidor de processamento em GPU equipado com 8 unidades de processamento NVIDIA A100 e 2TB de memória RAM;
- Um sistema de armazenamento Lustre com 6 servidores de armazenamento em SSD/NVMe, totalizando 300TB de espaço disponível.

Com essa infraestrutura de hardware, o HPC Marvin é capaz de oferecer um ambiente de processamento robusto e eficiente para as necessidades computacionais dos usuários.

### Sistema Operacional

Nesta seção, descreveremos o sistema operacional utilizado no HPC Marvin, incluindo sua versão e principais recursos.

### Programas e Aplicativos

Aqui, forneceremos uma lista dos principais softwares instalados no HPC Marvin, como compiladores, bibliotecas e ferramentas de programação.

## Sistema de Filas 📋

Nesta seção, descreveremos o sistema de filas utilizado no HPC Marvin para gerenciar as solicitações de processamento dos usuários.

### Tipos de filas

Aqui, apresentaremos os diferentes tipos de filas disponíveis no HPC Marvin, incluindo filas para processamento de longa duração, filas para processamento de curta duração, dentre outras.

### Políticas de filas

Nesta seção, descreveremos as políticas de filas utilizadas no HPC Marvin para determinar a ordem em que as solicitações são processadas, incluindo a política de prioridade e a política de justiça.

### Submissão de trabalhos

Aqui, explicaremos como os usuários podem submeter seus trabalhos para o sistema de filas do HPC Marvin, incluindo as opções de configuração disponíveis.

### Monitoramento de trabalhos

Nesta seção, descreveremos como os usuários podem monitorar o status de seus trabalhos, incluindo informações sobre o tempo de execução e a utilização dos recursos do sistema.
