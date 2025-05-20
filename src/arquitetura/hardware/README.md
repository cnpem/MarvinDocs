# Hardware

O hardware do HPCC Marvin foi adquirido em 2022 da empresa [Atos](https://atos.net/pt-br/brasil-atos), com investimento aproximado de US$350000. O cluster está fisicamente instalado no Data Center do [Sirius/LNLS](https://lnls.cnpem.br/sirius/), contando com infraestrutura de refrigeração e energia.

O cluster é composto por um conjunto de servidores, chamados de nós, organizados conforme a topologia tradicional de um cluster HPC:

- `01` nó de login (_head node_): ponto de entrada dos usuários, onde comandos são executados e _jobs_ são submetidos.
- `01` nó de computação em CPU (_CPU node_): dedicado à execução de _jobs_ que requerem alto desempenho de processamento em CPU.
- `01` nó de computação em GPU (_GPU node_): dedicado à execução de _jobs_ que se beneficiam de aceleração por GPU.
- `01` sistema de armazenamento de alta performance (_high performance storage system_): sistema de arquivos compartilhado baseado em [Lustre](https://www.lustre.org/) , voltado para I/O paralelo de alta velocidade.

As especificações técnicas de cada nó estão apresentadas na tabela a seguir:

| Nó                       | CPU                              | RAM    | GPU                     | Armazenamento             |
|:------------------------:|:--------------------------------:|:------:|:-----------------------:|:-------------------------:|
| Login                    | AMD EPYC 7352 24-Core @ 2.4 GHz  | 256 GB | NVIDIA A40 (48 GB)      | N/A                       |
| CPU                      | AMD EPYC 7742 64-Core @ 2.25 GHz | 1 TB   | N/A                     | N/A                       |
| GPU                      | AMD EPYC 7742 64-Core @ 2.25 GHz | 2 TB   | 8x NVIDIA A100 (40 GB)  | N/A                       |
| Storage HPC              | N/A                              | N/A    | N/A                     | 300 TB                    |
