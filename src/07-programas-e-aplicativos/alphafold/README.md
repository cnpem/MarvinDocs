# AlphaFold

O [AlphaFold](https://alphafold.ebi.ac.uk/) é um programa de modelagem de estrutura proteicas utilizando redes neurais artificiais (_Deep Learning_). Além de proteínas individuais, ele também permite modelar multímeros e complexos.

Para mais informações sobre o AlphaFold, acesse <https://github.com/deepmind/alphafold/>.

## Como executar o AlphaFold no HPCC Marvin

Para executar o AlphaFold, são necessários os seguintes passos:

1. Crie uma pasta contendo o arquivo FASTA da(s) proteína(s) que deseja modelar. Exemplo: `fasta_dir`.

2. Crie um script de submissão no SLURM através do `sbatch`

Abaixo, está o conteúdo de um script de submissão (p. ex. `sbatch nova_tarefa_alphafold.sh`) do job no SLURM:

```bash
#!/bin/sh
#SBATCH --job-name=alphafold
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --partition=short-gpu-small
#SBATCH --mem-per-cpu=8G
#SBATCH --gres=gpu:1g.5gb:1

# essa variável aponta para o banco de dados utilizado pelo alphafold (NÃO ALTERE)   
ALPHAFOLD_DB=/public/alphafold_db_20231114/

# imagem do singularity onde o alphafold está instalá-do (NÃO ALTERE)
ALPHAFOLD_SIF=/opt/images/alphafold/alphafold-2_3_2.sif

# essa variável aponta para o arquivo fasta (MUDE PARA O SEU ARQUIVO) 
FASTA_FILE=./fasta_dir/P01308.fasta

# nome da pasta onde os modelos e resultados serão salvos (PODE MUDAR PARA UM NOME QUE ESCOLHER)
OUTPUT_DIR=./results

# comando de execução do AlphaFold
singularity run --nv -B $ALPHAFOLD_DB:/database $ALPHAFOLD_SIF \
    --fasta_paths=$FASTA_FILE \
    --output_dir=$OUTPUT_DIR \
    --data_dir=/database/ \
    --template_mmcif_dir=/database/pdb_mmcif/mmcif_files/ \
    --obsolete_pdbs_path=/database/pdb_mmcif/obsolete.dat \
    --uniref90_database_path=/database/uniref90/uniref90.fasta \
    --mgnify_database_path=/database/mgnify/mgy_clusters_2018_12.fa \
    --pdb70_database_path=/database/pdb70/pdb70 \
    --uniclust30_database_path=/database/uniclust30/uniclust30_2018_08/uniclust30_2018_08 \
    --bfd_database_path=/database/bfd/bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt \
    --max_template_date=`date +'%Y-%m-%d'` \
    --use_gpu_relax 
```

3. Subsitua os valores das variáveis `ALPHAFOLD_SIF`, `FASTA_FILE` e `OUTPUT_DIR` conforme necessário. 

<div class="warning">

O <code>ALPHAFOLD_SIF</code> deve apontar para a imagem do Singularity do AlphaFold, que possui as seguintes versões:

- versão 2.3.2: `/opt/images/alphafold-2_3_2.sif`
- versão 2.2.4: `/opt/images/alphafold-2_2_4.sif`
- versão 2.2.3: `/opt/images/alphafold-2_2_3.sif`

O <code>FASTA_FILE</code> deve apontar para o arquivo FASTA da proteína que você deseja modelar.

O <code>OUTPUT_DIR</code> é onde os resultados serão salvos.
</div>

4. Submeta o script de submissão no SLURM. Você pode fazer isso através do comando `sbatch`:

```bash
sbatch nova_tarefa_alphafold.sh
```

Para verificar os argumentos aceitos pelo AlphaFold, você pode executar o seguinte comando:

```bash
singularity run /opt/images/alphafold/alphafold-2_3_2.sif --helpshort
```
