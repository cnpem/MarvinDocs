# Carregando imagens via OMERO.insight

O OMERO.insight é uma aplicação desktop que permite o gerenciamento e visualização de imagens armazenadas no servidor OMERO. Ele oferece uma interface gráfica amigável para navegar, visualizar e organizar suas imagens.

## Instalando o OMERO.insight

Para realizar o envio das imagens à plataforma OMERO, é necessário instalar o programa OMERO.insight no computador que será utilizado para esse procedimento. O instalador está disponível em: <https://www.openmicroscopy.org/omero/downloads/>.

<center>
<img src="imagens/omero-insight-download.png" alt="OMERO.insight download"  width="80%"/>
</center>

Escolha a versão mais recente disponível para o seu sistema operacional.

## Configurando o OMERO.insight

1. Após a instalação, abra o OMERO.insight em seu computador e clique no ícone de ferramenta (🔧), localizado no canto superior direito da janela. 

<center>
    <img src="imagens/omero-insight-gui.png" alt="OMERO.insight interface"  width="40%"/>
</center>

2. Em seguida, clique no botão (➕) para adicionar um novo endereço de plataforma OMERO;

<center>
    <img src="imagens/omero-insight-add-new-server.png" alt="OMERO.insight add server"  width="40%"/>
</center>

3. Na janela "Add new server", digite o seguinte endereço `omero-lnbio.cnpem.br` e clique em “⏎ OK”;

<center>
    <img src="imagens/omero-insight-add-address.png" alt="OMERO.insight add server"  width="40%"/>
</center>

4. Selecione o endereço omero-lnbio.cnpem.br e clique em “Apply” (Figura 5b);

<center>
    <img src="imagens/omero-insight-select-address.png" alt="OMERO.insight select server"  width="40%"/>
</center>

## Transferindo imagens para o OMERO

Após configurar o OMERO do LNBio no OMERO.insight, utilize suas credenciais institucionais do CNPEM para fazer login.

<center>
    <img src="imagens/omero-insight-login.png" alt="OMERO.insight login"  width="40%"/>
</center>

<div class="warning">
    Se você é a Marie Skłodowska-Curie, o seu usuário institucional é <code>marie.curie</code> em “Username” e sua senha institucional em “Password”.
</div>

Após o login, você terá acesso à interface do OMERO.insight, onde poderá visualizar e gerenciar suas imagens. 

<center>
    <img src="imagens/omero-insight-interface.png" alt="OMERO.insight main interface"  width="80%"/>
</center>

Para carregar novas imagens, siga os passos abaixo:

1. Clique no menu "File" e selecione "Import..."

<center>
    <img src="imagens/omero-insight-import.png" alt="OMERO.insight import menu"  width="80%"/>
</center>

2. Na janela de importação, selecione os arquivos que deseja carregar para o OMERO, e clique em `>` para colocá-los na fila de transferência.

<center>
    <img src="imagens/omero-insight-add-images.png" alt="OMERO.insight add images"  width="80%"/>
</center>

3. Uma janela para definir o projeto de destino aparecerá. Selecione o projeto desejado ou crie um novo, e clique em "Add to the Queue".

<center>
    <img src="imagens/omero-insight-add-to-queue.png" alt="OMERO.insight add to queue"  width="50%"/>
</center>

4. Ajuste as configurações de importação. Desmarque opção `Override default File naming`, e caso deseje acelerar o processo de transferência, ative todas as opções da área `Import Speedup`.

<center>
    <img src="imagens/omero-insight-select-options.png" alt="OMERO.insight select options"  width="80%"/>
</center>

5. Clique em "Import" para iniciar o processo de transferência das imagens para o OMERO.

<center>
    <img src="imagens/omero-insight-click-on-import.png" alt="OMERO.insight start import"  width="80%"/>
</center>

6. Durante a transferência, uma janela de progresso será exibida, indicando os arquivos que estão sendo transferidos para o OMERO.

<center>
    <img src="imagens/omero-insight-transfering.png" alt="OMERO.insight transfer progress"  width="80%"/>
</center>

7. Se a transferência for bem-sucedida, uma marcação verde (✔️) será exibido ao lado da aba ou no canto superior direito da tela inicial.

<center>
    <img src="imagens/omero-insight-transfered.png" alt="OMERO.insight transfer completed"  width="80%"/>
</center>

8. Após a conclusão da transferência, as imagens estarão disponíveis no menu de navegação no projeto definido no momento da importação. 

<center>
    <img src="imagens/omero-insight-images-on-omero.png" alt="OMERO.insight navigate to project"  width="80%"/>
</center>

Caso não apareçam imediatamente, clique no ícone de “Refresh” (🔄) para atualizar as placas importadas pelo OMERO.insight.

<center>
    <img src="imagens/omero-insight-refresh.png" alt="OMERO.insight refresh"  width="80%"/>
</center>
