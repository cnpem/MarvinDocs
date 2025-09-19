# Ilastik

O [Ilastik](https://www.ilastik.org/) é uma ferramenta de aprendizado de máquina interativa para análise de imagens, especialmente útil para tarefas como segmentação, classificação e rastreamento de objetos em imagens biológicas.

Para mais informações sobre o Ilastik, acesse <https://www.ilastik.org/documentation/>.

## Carregando o módulo

Para habilitar o Ilastik no HPCC Marvin, você deve carregar o módulo `ilastik`:

```bash
module load ilastik
```

<div class="warning">
    <br>As versões disponíveis do Ilastik no HPCC Marvin são:
    <ul>
        <li><code>ilastik/1.4.1    (D)</code></li>
         <li><code>ilastik/1.4.0     </code></li>
    </ul>
    Onde <code>(D)</code> indica a versão padrão.<br>
</div>

Para acessar a documentação do modulo, utilize:

```bash
module help ilastik
```

## Como executar o Ilastik no Open OnDemand

Para executar o Ilastik, são necessários os seguintes passos:

1. Acesse o Open OnDemand do HPCC Marvin em <https://marvin.cnpem.br/>.

2. Em `Interactive Apps`, abra uma `VNC`.

3. No formulário da VNC, selecione a partição `gui-gpu-small` e defina o número de horas, número de GPUs e número de CPUs conforme necessário. Clique em `Launch`.

4. Uma nova janela será aberta com a VNC. Aguarde até que a VNC esteja ativa (`Running`) e clique em `Launch VNC`.

5. Uma vez que a VNC estiver ativa, abra um terminal dentro da VNC.

6. No terminal, execute o seguinte comando para iniciar o Ilastik:

```bash
# Habilitar o módulo
module load ilastik
# Iniciar o Ilastik com interface gráfica
ilastik
```

## Submetendo jobs do Ilastik

O Ilastik também pode ser executado via submissão de jobs no SLURM, permitindo análises em segundo plano e melhor aproveitamento dos recursos do cluster. Crie um arquivo de script, por exemplo `ilastik.sh`, com o seguinte conteúdo:

```bash
#!/bin/bash
#SBATCH --job-name=ilastik
#SBATCH --partition=short-gpu-small 
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem-per-cpu=2GB
#SBATCH --gres=gpu:1g.5gb:1

module load ilastik

# Executar o Ilastik em modo headless (sem interface gráfica)
ilastik --headless --project proj.ilp
```

<div class="warning">
<br>Os parâmetros utilizados nesse comando são:
   <ul>
         <li><code>--headless</code>: Executa o Ilastik em modo CLI (sem interface gráfica).</li>
         <li><code>--project proj.ilp</code>: Especifica o caminho para o projeto que será executado.</li>
   </ul>
</div>

Para submeter o job, salve o script e utilize o comando `sbatch`:

```bash
sbatch ilastik.sh
```

Para mais detalhes sobre os parâmetros do Ilastik, use:

```bash
ilastik --help
```
