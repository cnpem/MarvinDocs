# Juicer

[Juicer](https://github.com/aidenlab/juicer) é um **pipeline completo para processamento e análise de dados Hi-C**, desenvolvido pelo **Aiden Lab**. Ele automatiza desde o **alinhamento das leituras** até a **geração de mapas de interação genômica** em múltiplas resoluções (arquivos **.hic**).

Útil para explorar estruturas 3D do genoma — como **TADs, loops** e **compartimentos** — o Juicer é amplamente adotado em **genômica estrutural**.  

Para mais informações: <https://github.com/aidenlab/juicer/wiki>

## Carregando o módulo

Para habilitar o juicer no HPCC Marvin, você deve carregar o módulo `juicer`:

```bash
module load juicer/<versão desejada>
```

<div class="warning">
    <br>As versões disponíveis do juicer no HPCC Marvin são:
    <ul>
        <li><code>juicer/2.0   (D)</code></li>
        <li><code>juicer/1.6</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help juicer
```

## Executando o módulo

O script principal do juicer é chamado com o comando `juicer.sh` e pode ser executado conforme o exemplo:

```bash
juicer.sh -z [reference genome file]
```

Para mais informações detalhadas sobre o script do juicer, acesse a [página de Usage do juicer](https://github.com/aidenlab/juicer/wiki/Usage).

Além do script principal, o módulo também conta com o pacote de ferramentas `juicer_tools`. Para obter informações sobre o uso e ajuda, execute:

```bash
juicer_tools -h
```

Para mais informações, acesse a [página de Quick Start do juicer tools](https://github.com/aidenlab/juicer/wiki/Juicer-Tools-Quick-Start).

Note que, na wiki do juicer tools, ele estará referenciado como juicebox_tools.jar e chama o java para executar o .jar. Isso não é necessário no Marvin, apenas passe as opções e comandos diretamente.

Por exemplo, caso você queira executar o seguinte comando que está na wiki do juicer tools:

```bash
java -Xmx2g -jar juicebox_tools.jar pre data/test.txt.gz data/test.hic hg19
```

No Marvin, você executaria da seguinte forma:

```bash
juicer_tools pre data/test.txt.gz data/test.hic hg19
```


## Submetendo jobs

A execução do juicer no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `juicer.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=juicer
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem-per-cpu=4GB

module load juicer/2.0

REFERENCE_GENOME="caminho/para/genome/file"

juicer.sh -z "$REFERENCE_GENOME"
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch juicer.sh
```

Para mais detalhes sobre os parâmetros do juicer, use:

```bash
juicer.sh -h
```
