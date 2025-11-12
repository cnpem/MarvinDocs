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

A execução do GROMACS no HPCC Marvin é feita por meio de scripts de submissão no SLURM. 

Por padrão, recomenda-se utilizar a fila `short-gpu-small` para execuções de pequeno e médio porte. Para isso, crie um arquivo de script, por exemplo `gromacs.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=gromacs
#SBATCH --partition=short-gpu-small
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem-per-cpu=2GB
#SBATCH --gres=gpu:1g.5gb:1
#SBATCH --time=24:00:00

# Load GROMACS module
module load gromacs/2024.5

# Run molecular dynamics simulation with GPU acceleration
gmx mdrun -s production.tpr -v -deffnm production -pin off -ntomp $SLURM_CPUS_PER_TASK -nb gpu -pme gpu -update gpu -bonded gpu
```

Para execuções de maior porte, utilize a fila `short-gpu-big` e ajuste os parâmetros de recursos conforme o exemplo abaixo:

```bash
#!/bin/bash
#SBATCH --job-name=gromacs
#SBATCH --partition=short-gpu-big
#SBATCH --ntasks=3
#SBATCH --cpus-per-task=8
#SBATCH --mem-per-cpu=2GB
#SBATCH --gres=gpu:a100:1
#SBATCH --time=24:00:00

# Load GROMACS module
module load gromacs/2024.5

# Run molecular dynamics simulation with GPU acceleration
gmx mdrun -s production.tpr -v -deffnm production -pin off -ntomp $SLURM_CPUS_PER_TASK -nb gpu -pme gpu -update gpu -bonded gpu
```

<div class="warning">
    Em ambos os cenários, ajuste os recursos computacionais (CPU, GPU, memória e tempo) conforme as necessidades do seu job.
</div>

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch gromacs.sh
```

Para mais detalhes sobre os comandos do GROMACS, use:

```bash
gmx help
```
