# TCRmodel2

O [TCRmodel2](https://academic.oup.com/nar/article/51/W1/W569/7151345) é um programa de predição de estrutura de proteínas baseado em adaptações do AlphaFold2. Apresenta alta acurácia de predição do complexo TCR:pMHC, assim como, estruturas unbound de TCRs. O tempo de predição (~15 minutos por complexo para as regiões variáveis) também é reduzido em comparação a outros modelos. As predições já possuem resíduos renumerados para o esquema AHo e cadeias renomeadas para MHC (A), peptídeo (C), TCRalpha (D) e TCRbeta (E).   

Para mais informações sobre TCRmodel2, acesse <https://github.com/piercelab/tcrmodel2>.

## Carregando o módulo

Para habilitar o TCRmodel2 no HPCC Marvin, você deve carregar o módulo `tcrmodel2`:

```bash
module load tcrmodel2
```

Para acessar a documentação do modulo, utilize:

```bash
module help tcrmodel2
```

## Executando o módulo

<div class="warning">
    <br>O banco de dados e pesos do AF2 estão na pasta <code>/public</code> do HPC e são necessários para execução dos scripts.</br>
</div>


O TCRmodel2 oferece dois principais scripts: 

- `run_tcrmodel2.py`: predição do complexo TCR:pMHC  que pode ser chamado com `tcrmodel2`
- `run_tcrmodel2_ub_tcr.py`: predição de estruturas unbound de TCRs que pode ser chamado com `tcrmodel2_ub_tcr`

Ambos scripts contém diferentes flags. Para obter informações sobre o uso de cada um, execute:

```
tcrmodel2 --help  #or
tcrmodel2_ub_tcr --help
```

## Submetendo jobs

A execução do TCRmodel2 no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Para modelar apenas o TCR unbound, crie um arquivo de script, por exemplo `tcrmodel2.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=tcrmodel2
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=6
#SBATCH --partition=short-gpu-small
#SBATCH --mem-per-cpu=8G
#SBATCH --gres=gpu:1g.5gb:5
#SBATCH --output=slurm.out
#SBATCH --error=slurm.error

ml load tcrmodel2

OUTPUT_DIR="/output"
TCRA="GQQVMQIPQYQHVQEGEDFTTYCNSSTTLSNIQWYKQRPGGHPVFLIQLVKSGEVKKQKRLTFQFGEAKKNSSLHITATQTTDVGTYFCAVSYGGSQGNLIFGKGTKLSVKP"
TCRB="DGGITQSPKYLFRKEGQNVTLSCEQNLNHDAMYWYRQDPGQGLRLIYYSQIVNDFQKGDIAEGYSVSREKKESFPLTVTSAQKNPTAFYLCASSIRSTDTQYFGPGTRLTVLE"

tcrmodel2_ub_tcr --job_id=test --output_dir=$OUTPUT_DIR --tcra_seq=$TCRA --tcrb_seq=$TCRB --ori_db=/database/ --tp_db=/opt/tcrmodel2/data/databases --relax_structures=True --max_template_date=2100-01-01
```
Ao carregar o módulo tcrmodel2, ficarão disponíveis dois comandos (**tcrmodel2** e **tcrmodel2_ub_tcr**) para modelar, respectivamente, o complexo inteiro ou somente TCRab. Lembrando que, para modelar o complexo inteiro, siga as instruções do repositório do TCRmodel2 para configurar as flags e substitua o comando `tcrmodel2_ub_tcr` por `tcrmodel2` no script do slurm.

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch tcrmodel2.sh
```

