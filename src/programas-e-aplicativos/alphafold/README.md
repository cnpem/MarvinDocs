# AlphaFold

O AlphaFold é um software de modelagem de estrutura proteicas utilizando redes neurais artificiais (_Deep Learning_).
Ele também é capaz de modelar multímeros e complexos.

Para mais informações sobre o uso do AlphaFold acesse o [repositório](
https://github.com/deepmind/alphafold/).

Abaixo descrevemos resumidamente como rodar o AlphaFold no **MARVIN** (hpc-lnbio.cnpem.br). Está nos planos tornar a 
tarefa mais fácil e amigável aos usuários, por isso, essa página irá mudar ao longo do tempo. 

## Como usar

Para utilizar o AlphaFold são necessários os seguintes passos:

1. criar uma pasta contendo o arquivo fasta da(s) proteína(s) para modelar. ex `fasta_dir`
2. criar um script da tarefa para submetê-la ao SLURM através do `sbatch`
     
Abaixo um exemplo da tarefa para submissão. Após salvar o arquivo (ex. `nova_tarefa_alphafold.sh`), fazemos a submissão para que ele entre na fila de execucão com o comando sbatch (ex. `sbatch nova_tarefa_alphafold.sh`). 

```bash
#!/bin/sh
#SBATCH --job-name=alphafold
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=32
#SBATCH --partition=short-gpu
#SBATCH --gpus=1

# essa variável aponta para o banco de dados utilizado pelo alphafold (NÃO ALTERE)   
ALPHAFOLD_DB=/public/alphafold_db_20220825

# imagem do singularity onde o alphafold está instalá-do (NÃO ALTERE)
ALPHAFOLD_SIF=/opt/images/alphafold/alphafold-2_2_4.sif

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
    --jackhmmer_binary_path=/opt/conda/bin/jackhmmer 
    --hhblits_binary_path=/opt/conda/bin/hhblits \
    --hhsearch_binary_path=/opt/conda/bin/hhsearch \
    --kalign_binary_path=/opt/conda/bin/kalign \
    --use_gpu_relax \
    --max_template_date=`date +'%Y-%m-%d'`
```

Abaixo estão os argumentos aceitos pelo AlphaFold.

```bash
Full AlphaFold protein structure prediction script.
flags:

/opt/alphafold/run_alphafold.py:
  --[no]benchmark: Run multiple JAX model evaluations to obtain a timing that
    excludes the compilation time, which should be more indicative of the time
    required for inferencing many proteins.
    (default: 'false')
  --bfd_database_path: Path to the BFD database for use by HHblits.
  --data_dir: Path to directory of supporting data.
  --db_preset: <full_dbs|reduced_dbs>: Choose preset MSA database configuration
    - smaller genetic database config (reduced_dbs) or full genetic database
    config  (full_dbs)
    (default: 'full_dbs')
  --fasta_paths: Paths to FASTA files, each containing a prediction target that
    will be folded one after another. If a FASTA file contains multiple
    sequences, then it will be folded as a multimer. Paths should be separated
    by commas. All FASTA paths must have a unique basename as the basename is
    used to name the output directories for each prediction.
    (a comma separated list)
  --hhblits_binary_path: Path to the HHblits executable.
    (default: '/opt/conda/bin/hhblits')
  --hhsearch_binary_path: Path to the HHsearch executable.
    (default: '/opt/conda/bin/hhsearch')
  --hmmbuild_binary_path: Path to the hmmbuild executable.
    (default: '/opt/conda/bin/hmmbuild')
  --hmmsearch_binary_path: Path to the hmmsearch executable.
    (default: '/opt/conda/bin/hmmsearch')
  --jackhmmer_binary_path: Path to the JackHMMER executable.
    (default: '/opt/conda/bin/jackhmmer')
  --kalign_binary_path: Path to the Kalign executable.
    (default: '/opt/conda/bin/kalign')
  --max_template_date: Maximum template release date to consider. Important if
    folding historical test sets.
  --mgnify_database_path: Path to the MGnify database for use by JackHMMER.
  --model_preset: <monomer|monomer_casp14|monomer_ptm|multimer>: Choose preset
    model configuration - the monomer model, the monomer model with extra
    ensembling, monomer model with pTM head, or multimer model
    (default: 'monomer')
  --num_multimer_predictions_per_model: How many predictions (each with a
    different random seed) will be generated per model. E.g. if this is 2 and
    there are 5 models then there will be 10 predictions per input. Note: this
    FLAG only applies if model_preset=multimer
    (default: '5')
    (an integer)
  --obsolete_pdbs_path: Path to file containing a mapping from obsolete PDB IDs
    to the PDB IDs of their replacements.
  --output_dir: Path to a directory that will store the results.
  --pdb70_database_path: Path to the PDB70 database for use by HHsearch.
  --pdb_seqres_database_path: Path to the PDB seqres database for use by
    hmmsearch.
  --random_seed: The random seed for the data pipeline. By default, this is
    randomly generated. Note that even if this is set, Alphafold may still not
    be deterministic, because processes like GPU inference are nondeterministic.
    (an integer)
  --[no]run_relax: Whether to run the final relaxation step on the predicted
    models. Turning relax off might result in predictions with distracting
    stereochemical violations but might help in case you are having issues with
    the relaxation stage.
    (default: 'true')
  --small_bfd_database_path: Path to the small version of BFD used with the
    "reduced_dbs" preset.
  --template_mmcif_dir: Path to a directory with template mmCIF structures, each
    named <pdb_id>.cif
  --uniclust30_database_path: Path to the Uniclust30 database for use by
    HHblits.
  --uniprot_database_path: Path to the Uniprot database for use by JackHMMer.
  --uniref90_database_path: Path to the Uniref90 database for use by JackHMMER.
  --[no]use_gpu_relax: Whether to relax on GPU. Relax on GPU can be much faster
    than CPU, so it is recommended to enable if possible. GPUs must be available
    if this setting is enabled.
  --[no]use_precomputed_msas: Whether to read MSAs that have been written to
    disk instead of running the MSA tools. The MSA files are looked up in the
    output directory, so it must stay the same between multiple runs that are to
    reuse the MSAs. WARNING: This will not check if the sequence, database or
    configuration have changed.
    (default: 'false')
```
