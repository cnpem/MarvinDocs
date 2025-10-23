# pyGenomeTracks

O [pyGenomeTracks](https://github.com/deeptools/pyGenomeTracks) é uma ferramenta para **gerar visualizações integradas de dados genômicos** a partir de múltiplas faixas (*tracks*), como Hi-C, ChIP-seq, RNA-seq, entre outros.  
Ele permite criar gráficos de alta qualidade combinando várias camadas de informação em uma única figura, facilitando a interpretação e comparação de diferentes experimentos genômicos.

Para mais informações, acesse: <https://github.com/deeptools/pyGenomeTracks>

## Carregando o módulo

Para habilitar o pyGenomeTracks no HPCC Marvin, você deve carregar o módulo `pyGenomeTracks`:

```bash
module load pyGenomeTracks
```

<div class="warning">
    <br>As versões disponíveis do pyGenomeTracks no HPCC Marvin são:
    <ul>
        <li><code>pyGenomeTracks/3.9  (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help pyGenomeTracks
```

## Executando o módulo

Para executar o **pyGenomeTracks**, é necessário um arquivo de configuração que descreva as *tracks* (faixas de dados).  
A maneira mais fácil de criar esse arquivo é usando o programa `make_tracks_file`, que gera uma configuração padrão facilmente editável.  

Comando para criar o arquivo de configuração:

```bash
make_tracks_file --trackFiles <file1.bed> <file2.bw> ... -o tracks.ini
```

O `make_tracks_file` identifica automaticamente o tipo de arquivo com base em sua extensão.

Comando para gerar o gráfico de uma região genômica:

```bash
pyGenomeTracks --tracks tracks.ini --region chr2:10,000,000-11,000,000 --outFileName nice_image.pdf
```

A opção `--outFileName` define o formato da imagem de saída. Se for usado `.pdf`, o resultado será um arquivo PDF. Os formatos disponíveis são **pdf**, **png** e **svg**.

## Submetendo jobs

A execução do pyGenomeTracks no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `pyGenomeTracks.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=pyGenomeTracks
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem-per-cpu=2GB

module load pyGenomeTracks/3.9

TRACKS="/caminho/para/tracks/file"
REGION="chr2:10,000,000-11,000,000"
OUTPUT_FILE="out.pdf"

pyGenomeTracks --tracks "$TRACKS" --region "$REGION" --outFileName "$OUTPUT_FILE"

```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch pyGenomeTracks.sh
```

Para mais detalhes sobre os parâmetros do pyGenomeTracks, use:

```bash
pyGenomeTracks -h
```
