# AlphaFold

O [AlphaFold](https://alphafold.ebi.ac.uk/) é um programa de modelagem de estrutura proteicas utilizando redes neurais artificiais (_Deep Learning_). Além de proteínas individuais, ele também permite modelar multímeros e complexos.

Para mais informações sobre o AlphaFold, acesse <https://github.com/deepmind/alphafold/>.

## Carregando o módulo

Para habilitar o AlphaFold no HPCC Marvin, você deve carregar o módulo `alphafold`:

```bash
module load alphafold
```

<div class="warning">
    <br>As versões disponíveis do AlphaFold no HPCC Marvin são:
    <ul>
        <li><code>alphafold/2.3.2    (D)</code></li>
    </ul>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help alphafold
```

## Submetendo jobs

A execução do AlphaFold no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `alphafold.sh`, com o seguinte conteúdo:

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
<br>O <code>FASTA_FILE</code> deve apontar para o arquivo FASTA da proteína que você deseja modelar. O <code>OUTPUT_DIR</code> é onde os resultados serão salvos.<br>
</div>

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch alphafold.sh
```

Para mais detalhes sobre as opções do AlphaFold, use:

```bash
alphafold --helpshort
```
