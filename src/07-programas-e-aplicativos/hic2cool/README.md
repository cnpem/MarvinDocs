# hic2cool

O [hic2cool](https://github.com/4dn-dcic/hic2cool/) é uma ferramenta leve para **converter matrizes de contato Hi-C** do formato `.hic` para o formato `.cool`.
Ele suporta arquivos de resolução única ou múltiplas resoluções, permitindo integrar facilmente dados Hi-C com outras ferramentas de análise e visualização.

O hic2cool pode ser utilizado tanto como pacote Python em scripts quanto como ferramenta de linha de comando, oferecendo flexibilidade para pipelines automatizados de processamento de dados Hi-C.

Para mais informações, acesse: <https://github.com/4dn-dcic/hic2cool/>

## Carregando o módulo

Para habilitar o hic2cool no HPCC Marvin, você deve carregar o módulo `hic2cool`:

```bash
module load hic2cool
```

<div class="warning">
    <br>As versões disponíveis do hic2cool no HPCC Marvin são:
    <ul>
        <li><code>hic2cool/1.0.1   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help hic2cool
```

## Executando o módulo

O hic2cool possui diferentes modos que devem ser selecionados ao executá-lo. Segue um exemplo de `convert`:

```bash
hic2cool convert <infile> <outfile> -r <resolution> -p <nproc>
```

Consulte todos os modos de execução disponíveis com `hic2cool -h` e mais informações na [no repositório do hi2cool](https://github.com/4dn-dcic/hic2cool/).

## Submetendo jobs

A execução do hic2cool no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `hic2cool.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=hic2cool
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem-per-cpu=2GB

module load hic2cool/1.0.1

INPUT_FILE="/caminho/para/input/file"
OUTPUT_FILE="/caminho/para/input/file"
RESOLUTION=0
NPROC=1

hic2cool convert "$INPUT_FILE" "$OUTPUT_FILE" -r "$RESOLUTION" -p "$NPROC"
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch hic2cool.sh
```

Para mais detalhes sobre os parâmetros do hic2cool, use:

```bash
hic2cool -h
```
