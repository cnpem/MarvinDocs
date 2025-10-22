# Circos

O [Circos](https://circos.ca/) é um pacote de software para visualização de dados e informações em um **layout circular**.  
Ele é comumente utilizado para visualização de dados genômicos e criação de gráficos complexos, como:

- Rearranjos genômicos
- Conexões genômicas  
- Mapas de calor (heatmaps) e gráficos de dispersão  
- Relações de dados em layouts circulares  

Para mais informações sobre o Circos, acesse: https://circos.ca/

## Carregando o módulo

Para habilitar o Circos no HPCC Marvin, você deve carregar o módulo `circos`:

```bash
module load circos
```

<div class="warning">
    <br>As versões disponíveis do Circos no HPCC Marvin são:
    <ul>
        <li><code>circos/0.69-10   (D)</code></li>
    </ul> 
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help circos
```

## Configurando o módulo

O Circos gera imagens estáticas e o processo de geração das imagens é gerenciado por um arquivo de configurações central. Esse arquivo geralmente importa outros arquivos de configurações, como preferências de fonte e cores.

<div class="warning">
<br>Para executar o Circos, é necessário passar como argumento um arquivo de configuração com a flag <code>-conf [conf_file]</code>.

Acesse [Circos: Configuration files](https://circos.ca/documentation/tutorials/configuration/configuration_files/) para mais informações sobre sintaxe dos arquivos de configuração e como organizar os blocos.<br>
</div>

Durante a execução, caso não seja explicitamente definido o arquivo de configuração, o Circos buscará automaticamente por um `circos.conf` nos seguintes caminhos (entre outros):

```
./circos.conf
./etc/circos.conf
./../etc/circos.conf
```

Acesse [Circos: Runtime parameters](https://circos.ca/tutorials/lessons/configuration/runtime_parameters/) para mais informações.

O módulo contém o diretório `example` que pode ser utilizado como referência e para testar a execução do mesmo.

Você pode copiar o diretório para o seu home e executar o circos a partir dele, por exemplo:

```bash
cd ~
cp -r /opt/images/apps/circos/v0.69-10/example .
cd example
circos
```

## Submetendo jobs

A execução do Circos no HPCC Marvin é feita por meio de scripts de submissão no SLURM. Crie um arquivo de script, por exemplo `circos.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=circos
#SBATCH --partition=short-cpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem-per-cpu=2GB

module load circos/0.69-10

CONFIG_FILE="/caminho/para/circos.conf"

circos -conf "$CONFIG_FILE"
```

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch circos.sh
```

Para mais detalhes sobre os parâmetros do Circos, use:

```bash
circos --help
```
