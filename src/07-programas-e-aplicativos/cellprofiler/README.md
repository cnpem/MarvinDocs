# Cellprofiler

O [CellProfiler](https://github.com/CellProfiler/CellProfiler) é um programa de código aberto amplamente utilizado para análise de imagens biológicas. Ele permite a quantificação de características celulares em imagens, facilitando a análise de grandes conjuntos de dados.

Para mais informações sobre o CellProfiler, acesse <https://cellprofiler.org/>.

## Como executar o CellProfiler no Open OnDemand

Para executar o CellProfiler, são necessários os seguintes passos:

1. Acesse o Open OnDemand do HPCC Marvin em <https://marvin.cnpem.br/>.

2. Em `Interactive Apps`, abra uma `VNC`.

3. No formulário da VNC, selecione a partição `gui-gpu-small` e defina o número de horas, número de GPUs e número de CPUs conforme necessário. Clique em `Launch`.

4. Uma nova janela será aberta com a VNC. Aguarde até que a VNC esteja ativa (`Running`) e clique em `Launch VNC`.

5. Uma vez que a VNC estiver ativa, abra um terminal dentro da VNC.

6. No terminal, execute o seguinte comando para iniciar o CellProfiler:

   ```bash
   singularity run --nv /opt/images/cellprofiler/cellprofiler-4_2_6.sif ~/Desktop/session.out
   ```

<div class="warning">

O CellProfiler possui as seguintes versões disponíveis:

- versão 4.2.6: `/opt/images/cellprofiler-4_2_6.sif`
- versão 4.2.4: `/opt/images/cellprofiler-4_2_4.sif`

</div>

Além disso, você também pode executar a CLI do CellProfiler diretamente no terminal (sem interface gráfica), utilizando o seguinte comando:

```bash
singularity run --nv /opt/images/cellprofiler/cellprofiler-4_2_6.sif -c -r -p proj.cppipe
```

<div class="warning">
Os parâmetros utilizados nesse comando são:

- <code>-c</code>: Executa o CellProfiler em modo CLI (sem interface gráfica).
- <code>-r</code>: Executa o pipeline na inicialização.
- <code>-p</code>: Especifica o caminho para o pipeline que será executado (`proj.cppipe`).

</div>
