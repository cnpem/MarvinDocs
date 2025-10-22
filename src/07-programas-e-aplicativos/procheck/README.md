# Procheck
O [Procheck](https://www.ebi.ac.uk/thornton-srv/software/PROCHECK/) é um pacote de software para **avaliar a qualidade geométrica de estruturas de proteínas**.  
Ele é comumente utilizado para verificar parâmetros como:

- Geometria dos resíduos (ângulos phi/psi)
- Validação de ligações de hidrogênio e distâncias
- Conformidade de resíduos com estruturas cristalográficas conhecidas
- Geração de gráficos de qualidade e relatórios detalhados

Para mais informações sobre o PROCHECK, acesse <https://www.ebi.ac.uk/thornton-srv/software/PROCHECK/>

## Carregando o módulo

Para habilitar o PROCHECK no HPCC Marvin, você deve carregar o módulo `procheck`:

```bash
module load procheck 
```

<div class="warning">
    <br>As versões disponíveis do Procheck no HPCC Marvin são:
    <ul>
        <li><code>procheck/3.5.4 (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help procheck 
```

## Configurando o módulo
O **PROCHECK** inclui várias ferramentas e scripts, como:

- **procheck** — avaliação geral de estruturas  
- **procheck-nmr** — avaliação de estruturas NMR  
- **procheck-comp** — comparação de conformações

Ao carregar o módulo com `module load procheck`, é automaticamente executado um script para configuração de variáveis e alias que chamarão os diferentes binários do pacote. O script verifica qual o shell do usuário (bash/zsh ou csh/tcsh) e realiza a configuração de acordo.

Os alias atualmente configurados pelo script são:

```bash
prodir='/opt/images/apps/procheck/v3.5.4'
export prodir
alias procheck=$prodir'/procheck.scr'
alias procheck_comp=$prodir'/procheck_comp.scr'
alias procheck_nmr=$prodir'/procheck_nmr.scr'
alias proplot=$prodir'/proplot.scr'
alias proplot_comp=$prodir'/proplot_comp.scr'
alias proplot_nmr=$prodir'/proplot_nmr.scr'
alias aquapro=$prodir'/aquapro.scr'
alias gfac2pdb=$prodir'/gfac2pdb.scr'
alias viol2pdb=$prodir'/viol2pdb.scr'
alias wirplot=$prodir'/wirplot.scr'
```

Para mais informações sobre os diferentes scripts e programas do Procheck, consulte o [Manual](https://www.ebi.ac.uk/thornton-srv/software/PROCHECK/manual) e o [NMR Manual](https://www.ebi.ac.uk/thornton-srv/software/PROCHECK/nmr_manual)



## Submetendo jobs

A execução do Procheck no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `procheck.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=procheck
#SBATCH --partition=short-gpu-small
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem-per-cpu=2GB

module load procheck/3.5.4

EXAMPLE_FILE="/data/pdb/p1amt.pdb"  # the coordinates file in Brookhaven format
CHAIN="A"                           # an optional one-letter chain-ID
RESOLUTION=1.5                      # a real number giving the resolution of the structure

procheck "$EXAMPLE_FILE" "$CHAIN" "$RESOLUTION"
```

<div class="warning">
<br>O script acima funciona para o procheck básico. Caso queira executar o <strong>procheck_nmr</strong> ou <strong>procheck_comp</strong>, por exemplo, adapte as variáveis e argumentos de acordo com seus respectivos usos.<br>
</div>


Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch procheck.sh
```

Para mais detalhes sobre os parâmetros do Procheck, use:

```bash
procheck --help
```
