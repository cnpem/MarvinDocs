# Boltz-2

O [Boltz-2](https://boltz.bio/) é um modelo para predição de interação biomolecular. Boltz-2 vai além AlphaFold3 e Boltz-1 ao juntar modelagem de complexa estruturas e afinidade de ligantes, um componente crítico para o design molecular preciso.

Para mais informações sobre o Boltz-2, acesse <https://github.com/jwohlwend/boltz/tree/main/docs>.

## Carregando o módulo

Para habilitar o Boltz-2 no HPCC Marvin, você deve carregar o módulo `boltz`:

```bash
module load boltz
```
<div class="warning">
    <br>As versões disponíveis do Boltz no HPCC Marvin são:
    <ul>
        <li><code>boltz/2.1.1</code></li>
        <li><code>boltz/2.2.0</code></li>
        <li><code>boltz/2.2.1   (D)</code></li>
    </ul>
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do módulo, utilize:

```bash
module help boltz
```

### Submetendo jobs

A execução do Boltz no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `boltz.sh`, com o seguinte conteúdo:

```bash
#! /bin/bash
#SBATCH --job-name=boltz
#SBATCH --partition=short-gpu-big
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=8
#SBATCH --gres=gpu:a100:1
#SBATCH --mem=64G
#SBATCH --time=24:00:00

module load boltz

YAML_DIR="./yaml"
OUTPUT_DIR="./"
boltz \\
    predict \\
    $YAML_DIR \\
    --use_potentials \\
    --out_dir $OUTPUT_DIR
```

<div class="warning">
<br>O <code>YAML_DIR</code> deve apontar para o diretório que contém os arquivos.yaml ou ao .yaml da proteína que você deseja modelar ou predizer afinidade. O <code>OUTPUT_DIR</code> é onde os resultados serão salvos.<br>
</div>

Para submeter o job, salve o script e utilize o comando `sbatch`

```bash
sbatch boltz.sh
```

Para mais detalhes sobre parâmetros de configuração do boltz, use:

```bash
boltz predict --help
```

Para mais informações sobre configuração do yaml, cheque:
<https://github.com/jwohlwend/boltz/blob/main/docs/prediction.md>


Exemplo de YAML de configuração:
```yaml
sequences:
- protein:
    id: A 
    sequence: ANPCCSNPCQNRGECMSTGFDQYKCDCTRTGFYGENCTTPEFLTRIKLLLKPTPNTVHYILTHFKGVWNIVNNIPFLRSLIMKYVLTSRSYLIDSPPTYNVHYGYKSWEAFSNLSYYTRALPPVADDCPTPMGVKGNKELPDSKEVLEKVLLRREFIPDPQGSNMMFAFFAQHFTHQFFKTDHKRGPGFTRGLGHGVDLNHIYGETLDRQHKLRLFKDGKLKYQVIGGEVYPPTVKDTQVEMIYPPHIPENLQFAVGQEVFGLVPGLMMYATIWLREHNRVCDILKQEHPEWGDEQLFQTSRLILIGETIKIVIEDYVQHLSGYHFKLKFDPELLFNQQFQYQNRIASEFNTLYHWHPLLPDTFNIEDQEYSFKQFLYNNSILLEHGLTQFVESFTRQIAGRVAGGRNVPIAVQAVAKASIDQSREMKYQSLNEYRKRFSLKPYTSFEELTGEKEMAAELKALYSDIDVMELYPALLVEKPRPDAIFGETMVELGAPFSLKGLMGNPICSPQYWKPSTFGGEVGFKIINTASIQSLICNNVKGCPFTSFNVQ
    msa: ./msa/msa.a3m
- ligand:
    id: B
    smiles: COc1ccc(C2C(=O)c3ccccc3C2=O)cc1
constraints:
- pocket:
    binder: B
    contacts:
    - - A
      - 492
    - - A
      - 318
    max_distance: 6
    force: true
properties:
- affinity:
    binder: B
```
