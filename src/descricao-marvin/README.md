# Descrição do HPC Marvin

## Hardware

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

## Sistema Operacional

O sistema operacional utilizado no Marvin é o Rocky Linux 8.5.

## Programas e Aplicativos

Os usuários são estimulados a utilizarem programas instalados em containers [Singularity](https://docs.sylabs.io/guides/3.5/user-guide/introduction.html) ou em ambientes virtuais como conda.

Em `/opt/images` o usuário encontrará imagens do singularity (.sif) para algumas aplicações. Essas imagens foram feitas pela nossa equipe ou por usuários. Aliás, ficamos muito felizes quando usuários pedem para compartilharmos as imagens que eles criaram!
