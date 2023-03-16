# OpenFold

## Como usar

```bash
#!/bin/sh
#SBATCH --job-name=openfold
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --partition=short-gpu
#SBATCH --gpus=1

module load openfold

ALPHAFOLD_DB=/public/alphafold_db_20220825

singularity run --nv -B $ALPHAFOLD_DB:/database /opt/images/openfold.sif \
        ./fasta_dir \
        /database/pdb_mmcif/mmcif_files/ \
        --uniref90_database_path /database/uniref90/uniref90.fasta \
        --mgnify_database_path /database/mgnify/mgy_clusters_2018_12.fa \
        --pdb70_database_path /database/pdb70/pdb70 \
        --uniclust30_database_path /database/uniclust30/uniclust30_2018_08/uniclust30_2018_08 \
        --output_dir ./results \
        --bfd_database_path /database/bfd/bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt \
        --model_device cuda:0 \
        --jackhmmer_binary_path /opt/conda/bin/jackhmmer \
        --hhblits_binary_path /opt/conda/bin/hhblits \
        --hhsearch_binary_path /opt/conda/bin/hhsearch \
        --kalign_binary_path /opt/conda/bin/kalign \
        --config_preset "model_1_ptm" \
        --openfold_checkpoint_path /database/openfold_params/finetuning_ptm_1.pt
```

```bash
usage: run_pretrained_openfold.py [-h]
                                  [--use_precomputed_alignments USE_PRECOMPUTED_ALIGNMENTS]
                                  [--output_dir OUTPUT_DIR]
                                  [--model_device MODEL_DEVICE]
                                  [--config_preset CONFIG_PRESET]
                                  [--jax_param_path JAX_PARAM_PATH]
                                  [--openfold_checkpoint_path OPENFOLD_CHECKPOINT_PATH]
                                  [--save_outputs] [--cpus CPUS]
                                  [--preset {reduced_dbs,full_dbs}]
                                  [--output_postfix OUTPUT_POSTFIX]
                                  [--data_random_seed DATA_RANDOM_SEED]
                                  [--skip_relaxation]
                                  [--multimer_ri_gap MULTIMER_RI_GAP]
                                  [--trace_model] [--subtract_plddt]
                                  [--uniref90_database_path UNIREF90_DATABASE_PATH]
                                  [--mgnify_database_path MGNIFY_DATABASE_PATH]
                                  [--pdb70_database_path PDB70_DATABASE_PATH]
                                  [--uniclust30_database_path UNICLUST30_DATABASE_PATH]
                                  [--bfd_database_path BFD_DATABASE_PATH]
                                  [--jackhmmer_binary_path JACKHMMER_BINARY_PATH]
                                  [--hhblits_binary_path HHBLITS_BINARY_PATH]
                                  [--hhsearch_binary_path HHSEARCH_BINARY_PATH]
                                  [--kalign_binary_path KALIGN_BINARY_PATH]
                                  [--max_template_date MAX_TEMPLATE_DATE]
                                  [--obsolete_pdbs_path OBSOLETE_PDBS_PATH]
                                  [--release_dates_path RELEASE_DATES_PATH]
                                  fasta_dir template_mmcif_dir

positional arguments:
  fasta_dir             Path to directory containing FASTA files, one sequence
                        per file
  template_mmcif_dir

optional arguments:
  -h, --help            show this help message and exit
  --use_precomputed_alignments USE_PRECOMPUTED_ALIGNMENTS
                        Path to alignment directory. If provided, alignment
                        computation is skipped and database path arguments are
                        ignored.
  --output_dir OUTPUT_DIR
                        Name of the directory in which to output the
                        prediction
  --model_device MODEL_DEVICE
                        Name of the device on which to run the model. Any
                        valid torch device name is accepted (e.g. "cpu",
                        "cuda:0")
  --config_preset CONFIG_PRESET
                        Name of a model config preset defined in
                        openfold/config.py
  --jax_param_path JAX_PARAM_PATH
                        Path to JAX model parameters. If None, and
                        openfold_checkpoint_path is also None, parameters are
                        selected automatically according to the model name
                        from openfold/resources/params
  --openfold_checkpoint_path OPENFOLD_CHECKPOINT_PATH
                        Path to OpenFold checkpoint. Can be either a DeepSpeed
                        checkpoint directory or a .pt file
  --save_outputs        Whether to save all model outputs, including
                        embeddings, etc.
  --cpus CPUS           Number of CPUs with which to run alignment tools
  --preset {reduced_dbs,full_dbs}
  --output_postfix OUTPUT_POSTFIX
                        Postfix for output prediction filenames
  --data_random_seed DATA_RANDOM_SEED
  --skip_relaxation
  --multimer_ri_gap MULTIMER_RI_GAP
                        Residue index offset between multiple sequences, if
                        provided
  --trace_model         Whether to convert parts of each model to TorchScript.
                        Significantly improves runtime at the cost of lengthy
                        'compilation.' Useful for large batch jobs.
  --subtract_plddt      "Whether to output (100 - pLDDT) in the B-factor
                        column instead of the pLDDT itself
  --uniref90_database_path UNIREF90_DATABASE_PATH
  --mgnify_database_path MGNIFY_DATABASE_PATH
  --pdb70_database_path PDB70_DATABASE_PATH
  --uniclust30_database_path UNICLUST30_DATABASE_PATH
  --bfd_database_path BFD_DATABASE_PATH
  --jackhmmer_binary_path JACKHMMER_BINARY_PATH
  --hhblits_binary_path HHBLITS_BINARY_PATH
  --hhsearch_binary_path HHSEARCH_BINARY_PATH
  --kalign_binary_path KALIGN_BINARY_PATH
  --max_template_date MAX_TEMPLATE_DATE
  --obsolete_pdbs_path OBSOLETE_PDBS_PATH
  --release_dates_path RELEASE_DATES_PATH
```
