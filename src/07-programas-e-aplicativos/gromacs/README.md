# GROMACS

O [GROMACS](http://www.gromacs.org/) (GROningen MAchine for Chemical Simulations) é um conjunto de softwares livres e de código aberto para simulação e análise de dinâmica molecular. Ele é amplamente utilizado para o estudo de sistemas biológicos, como proteínas, lipídios e ácidos nucleicos, mas também pode ser aplicado a sistemas não biológicos.

Para mais informações sobre o GROMACS, acesse <https://manual.gromacs.org/current/index.html/>.

## Carregando o módulo

Para habilitar o GROMACS no HPCC Marvin, você deve carregar o módulo `gromacs`:

```bash
module load gromacs
```

<div class="warning">
    <br>As versões disponíveis do GROMACS no HPCC Marvin são:
    <ul>
        <li><code>gromacs/2024.5 (D)</code></li>
    </ul>
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help gromacs
```

## Submetendo jobs

A execução do GROMACS no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `gromacs.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=gromacs
#SBATCH --partition=short-gpu-big
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --gres=gpu:a100:1
#SBATCH --mem-per-cpu=2GB
#SBATCH --time=5-00:00:00

# Load GROMACS module
module load gromacs/2024.5

# Export necessary environment variables
export GMX_FORCE_UPDATE_DEFAULT_GPU=true

gmx mdrun -s production.tpr -v -deffnm production -pin on -ntomp $SLURM_CPUS_PER_TASK -nb gpu -pme gpu -update gpu -bonded gpu
```

<div class="warning">
    <br>A partição <code>short-gpu-small</code> também pode ser utilizada para execuções de menor porte. Ajuste os parâmetros de recursos conforme a necessidade do seu job.<br>
    <br>
</div>

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch gromacs.sh
```

Para mais detalhes sobre os comandos do GROMACS, use:

```bash
gmx help
```
