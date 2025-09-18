# AlphaFold

O [AlphaFold](https://alphafold.ebi.ac.uk/) é um programa de modelagem de estrutura proteicas utilizando redes neurais artificiais (_Deep Learning_). Além de proteínas individuais, ele também permite modelar multímeros e complexos.

Para mais informações sobre o AlphaFold, acesse <https://github.com/deepmind/alphafold/>.

## Como executar o AlphaFold no HPCC Marvin

Para habilitar o AlphaFold no HPCC Marvin, você deve carregar o módulo `alphafold`:

```bash
module load alphafold
```

<div class="warning">
    As versões disponíveis do AlphaFold no HPCC Marvin são:
    <ul>
        <li>2.3.2 (padrão)</li>
    </ul>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help alphafold
```

Para submeter _jobs_ do AlphaFold no HPCC Marvin, é necessário criar um script de submissão no SLURM. Para isso, você pode usar um editor de texto para criar um arquivo de script, por exemplo, `alphafold.sh`.

Abaixo, está o conteúdo básico de um script de submissão (p. ex. `sbatch nova_tarefa_alphafold.sh`) do job no SLURM:

```bash
 #!/bin/bash
  #SBATCH --job-name=alphafold2
  #SBATCH --partition=short-gpu-big
  #SBATCH --nodes=1
  #SBATCH --ntasks-per-node=1
  #SBATCH --cpus-per-task=8
  #SBATCH --gres=gpu:a100:1
  #SBATCH --mem=64G
  #SBATCH --time=24:00:00

  module load alphafold/2.3.2

  OUTPUT_DIR="resultado_af2"
  FASTA_FILE="meu_target.fasta"

  alphafold \\
    --output_dir=$OUTPUT_DIR \\
    --fasta_paths=$FASTA_FILE \\
    --max_template_date=2023-11-01 \\
    --model_preset=monomer_ptm \\
    --db_preset=full_dbs
```

<div class="warning">
O <code>FASTA_FILE</code> deve apontar para o arquivo FASTA da proteína que você deseja modelar.
O <code>OUTPUT_DIR</code> é onde os resultados serão salvos.
</div>

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch alphafold.sh
```

Para mais detalhes sobre as opções do AlphaFold, use:

```bash
alphafold --helpshort
```
