# Ilastik

O [Ilastik](https://www.ilastik.org/) é uma ferramenta de aprendizado de máquina interativa para análise de imagens, especialmente útil para tarefas como segmentação, classificação e rastreamento de objetos em imagens biológicas.

Para mais informações sobre o Ilastik, acesse <https://www.ilastik.org/documentation/>.

## Como executar o Ilastik no Open OnDemand

Para executar o Ilastik, são necessários os seguintes passos:

1. Acesse o Open OnDemand do HPCC Marvin em <https://marvin.cnpem.br/>.

2. Em `Interactive Apps`, abra uma `VNC`.

3. No formulário da VNC, selecione a partição `gui-gpu-small` e defina o número de horas, número de GPUs e número de CPUs conforme necessário. Clique em `Launch`.

4. Uma nova janela será aberta com a VNC. Aguarde até que a VNC esteja ativa (`Running`) e clique em `Launch VNC`.

5. Uma vez que a VNC estiver ativa, abra um terminal dentro da VNC.

6. No terminal, execute o seguinte comando para iniciar o Ilastik:

   ```bash
   singularity run --nv /opt/images/ilastik/ilastik-1_4_0.sif
   ```

Além disso, você também pode executar a CLI do Ilastik diretamente no terminal (sem interface gráfica), utilizando o seguinte comando:

```bash
singularity run --nv /opt/images/ilastik/ilastik-1_4_0.sif --headless --project proj.ilp
```

<div class="warning">
Os parâmetros utilizados nesse comando são:
- `--headless`: Executa o Ilastik em modo CLI (sem interface gráfica).
- `--project`: Especifica o caminho para o projeto que será executado (`proj.ilp`).
</div>
