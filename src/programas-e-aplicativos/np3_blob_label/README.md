# NP3 Blob Label

## Introdução

## Como usar

### Criando Sbatch

```bash
#!/bin/bash
#SBATCH --job-name=NP3_BLOB_LABEL_your_intuitive_name
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --partition=short-gpu-small
#SBATCH --mem-per-cpu=4G

# altere o caminho abaixo para as pastas onde estão os dados
DATA_FOLDER=./Cristalografia/20230510_Bertonha/NP3_Blob_Label/NP3BlobLabel_05_2023/
# altere a linha abaixo para o caminho do arquivo csv
ENTRIES_LIST_PATH=./Cristalografia/20230510_Bertonha/NP3_Blob_Label/NP3BlobLabel_05_2023/NP3_Blob_Label_PBP1b_ref0_metadata.csv
# defina o nome da pasta de saída
OUTPUT_NAME=BlobLabel_Output
# altere a linha abaixo para o caminho da pasta de refinamento
REFINEMENT_PATH=./Cristalografia/20230510_Bertonha/NP3_Blob_Label/NP3BlobLabel_05_2023/


# Os comandos abaixos rodam os dois modelos do NP3 Blob Label
# O primeiro modelo é o AtomSymbolGroups
# O segundo modelo é o AtomC347CA56
# Caso queira rodar apenas um dos modelos, comente a linha correspondente ao outro modelo 
singularity run --nv /opt/images/NP3/blob_label/blob_label.sif \
  --model_ckpt_path /opt/np3_ligand/np3_blob_label/models/AtomSymbolGroups/modelAtomSymbolGroups_ligs-78911_img-qRankMask_5_gridspace-05_k1.ckpt \
  --data_folder $DATA_FOLDER \
  --entries_list_path $ENTRIES_LIST_PATH \
  --output_name $OUTPUT_NAME \
  --refinement_path $REFINEMENT_PATH

singularity run --nv /opt/images/NP3/blob_label/blob_label.sif \
  --model_ckpt_path /opt/np3_ligand/np3_blob_label/models/AtomC347CA56/modelAtomC347CA56_ligs-78911_img-qRankMask_5_gridspace-05_k13.ckpt \
  --data_folder $DATA_FOLDER \
  --entries_list_path $ENTRIES_LIST_PATH \
  --output_name $OUTPUT_NAME \
  --refinement_path $REFINEMENT_PATH
```