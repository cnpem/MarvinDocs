# Criando arquivo sbatch

Para usar o [NP³ MS Workflow](https://github.com/danielatrivella/NP3_MS_Workflow) no HPC MARVIN, a forma mais eficiente é submentendo um *job* no seu gerenciador de filas **slurm.**

Neste *job* colocamos todos os comandos que devem ser executados em um arquivo de texto simples de extesão `.sh`.

## Cabeçalho

No cabeçalho os principais parametros são:

- `--jobname=<jobname>` | Nome do seu *job*;
- `--ntaks=<numero>` | Número tarefas, geralmente 1 é suficiente;
- `--cpus-per-task=<numero>` | Número de CPUS que serão usadas, se usar um valor diferente de `1` lembre-se também modificar o parâmetro `-l` (é a letra éle) em seu `run`;
- `--partition=<nome_particao>` | O NP³ não é otimizado para GPU, então escolha uma das filas de CPU (que geralmente são menos concorridas, então pode ser uma vantagem). As fila de CPU atualmente disponíveis são:
  - debug-cpu | até 30:00 min | Recomendada para testes;
  - gui-cpu | até 12:00:00 horas | Recomendada para sessões VNC no OOD;
  - short-cpu | até  5-00:00:00  dias | Recomendada para maioria dos trabalhos;
  - long-cpu | até 15-00:00:0 dias | Recomendada para processamentos muito demorados.

Exemplo de cabeçalho:

```bash
#!/bin/bash
#SBATCH --job-name=NP3_MS_WORKFLOW_your_intuitive_name
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --partition=short-cpu
```

## Corpo

Para gerar o corpo deste processamento no MARVIN é obrigatório colocar ao menos **dois** comandos.

    1. A camada de memória chamada overlay;
    2. Os comandados de execução do NP³ (geralmente pre_process e/ou run).

### Camada de overlay

O Overlay é uma camada temporária de momória para armazenar temporariamente os arquivos de execução (mas não os de saída) do processamento.
Recomenda-se colocar como expaço um número cerca de 1,1 * o tamanho de sua pasta de mzxml.
Abaixo um exemplo para que se crie um overlay de 500 MB

```python
python3 /opt/images/NP3/ms_workflow/create_overlay.py 500
```

### Execução do NP³

Com o overlay criado, basta agora colocar o seu pre_process ou run.
Depois de ter enviado seus arquivos MZXML e metadado à sua área do OpenOnDemand, basta construir seu comando de processamento utilizando os endereços completos dos diretórios

Abaixo um exemplo para o run:

- Da usuário `marie.curie`;
- Saída no diretório `tmps` dentro de sua `home`;
- Com metadao em pasta de mzxml em `Documentos\NPTest`, também dentro da `home`;
- Tempos de tolerância de 1s para o mesmo batch e 2s geral;
- Verbose 10 que significa ligado para registro e ativa o teste de integridade no final (consulte o [manual](images/Manual_NP3_workflow.pdf) para mais opções).

Note que para quebrar a linha, e ficar mais legível, basta colcoar uma `\` logo antes da quebra que o programa interpreta como estivesse tudo na mesma linha

```bash
singularity exec --overlay $HOME/overlay.img /opt/images/NP3/ms_workflow/np3.sif \
node /opt/NP3_MS_Workflow/np3_workflow.js run \
-n NPTrial \
-o /home/marie.curie/tmps/ \
-m /home/marie.curie/Documentos/NPTest/marine_bacteria_lib_metadata.csv \
-d /home/luiz.alves/Documentos/NPTest/mzxml \
-t 1,2 \
-v 10
```

## Arquivo final

Ao final, juntando tudo, temos arquivo como o abaixo que pode ser colocando em um arquivo `my_np3_awsome_run.sh` e ser enviado ao slurm com o comando

```bash
sbatch my_np3_awsome_run.sh
```

Conteúdo final do `my_np3_awsome_run.sh`:

```bash
#!/bin/bash
#SBATCH --job-name=NP3_MS_WORKFLOW_your_intuitive_name
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --partition=short-cpu
#SBATCH --mem-per-cpu=4G

# Execute o script Python create_overlay.py 500 MB de espaço
python3 /opt/images/NP3/ms_workflow/create_overlay.py 500

# Execute a imagem Singularity com o comado NP3 e a juncao do overlay
singularity exec --overlay $HOME/overlay.img /opt/images/NP3/ms_workflow/np3.sif \
node /opt/NP3_MS_Workflow/np3_workflow.js run \
-n NPTrial \
-o /home/marie.curie/tmps/ \
-m /home/marie.curie/Documentos/NPTest/marine_bacteria_lib_metadata.csv \
-d /home/luiz.alves/Documentos/NPTest/mzxml \
-t 1,2 \
-v 10
```
