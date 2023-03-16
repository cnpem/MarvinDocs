# Primeiros Passos

Antes de começar a utilizar o HPC Marvin, é importante seguir alguns passos iniciais para garantir que tudo esteja configurado corretamente. Este capítulo irá guiá-los pelos primeiros passos necessários para começar a utilizar o sistema.

Para ativar seu usuário no sistema no HPC Marvin é preciso, fazer um primeiro acesso via terminal no `ssh` (Secury SHell), que é um protocolo de rede seguro que permite a comunicação com servidores remotos. Para se conectar ao sistema, siga as instruções abaixo.

Nos tutoriais, utilizaremos o <> para indicar variáveis. Sempre que aparecer algo entre <>, subistitua pelo valor adequado, (sem digitar o <>).

_Exemplo_: Se você é a Marie Skłodowska-Curie e seu usuário é marie.curie, ao ver `<seu.login.cnpem>@lnbio.cnmpem.br`, digite `marie.curie@lnbio.cnpem.br` para executar.

## Primeiro Acesso🚪

Para acessar o HPC Marvin, comece abrindo o terminal. Se estiver usando Windows, abra o PowerShell <img src="imagens/powershell_icon.png" alt="PowerShell logo" width="2%"></img>; se estiver usando Linux ou MacOS, abra o terminal <img src="imagens/terminal_icon.png" alt="Terminal logo" width="2.3%"></img>. Para acessar o HPC Marvin, use o comando:

```bash
ssh <seu.login.cnpem>@hpc-lnbio.cnpem.br
```

Se estiver no Windows e receber o seguinte erro, tente usar outro computador ou peça ajuda ao TIC para instalar o `ssh`.

```PowerShell
ssh: O termo 'ssh' não é reconhecido como nome de cmdlet, função, arquivo de script
ou programa operável. Verifique a grafia do nome ou, se um caminho tiver sido incluído,
veja se o caminho está correto e tente novamente.
Na linha:1 caractere:1
+ ssh marie.curie@hpc-lnbio.cnpem.br
+ ~~~
    + CategoryInfo          : ObjectNotFound (ssh:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```

Quando solicitado, digite sua **senha institucional**. Dependendo do seu terminal, você pode não ver nada na tela quando digita sua senha por motivos de segurança. Isso é normal. Se cometer algum erro, tente novamente.

Você pode receber um aviso solicitando sua confirmação antes de continuar conectando.

```bash
[...] Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Digite `yes` e pressione **enter**. Se tudo correu bem, você verá o cursor piscando no terminal, com um texto semelhante a:

```bash
[<seu.login.cnpem>@marvin ~]$
```

Digite o comando `ls` para verificar o conteúdo do diretório, e você deverá ver uma pasta chamada "ondemand". Confirme se a pasta está presente.

## Acesso pelo navegador <img src="imagens/browser_icons.png" alt="Browser Icons"  width="15%"></img>

Para acessar o cluster pelo navegador, abra o seu navegador e digite o seguinte endereço na barra de endereços:

```
https://hpc-lnbio.cnpem.br
```

Lembre-se, este site só estará disponível na rede interna. Para acessá-lo de fora do centro, é necessário usar a **VPN**. Caso não tenha este acesso à VPN, entre em contato com o **TIC**.

Na página que abrir, faça login com a sua **senha institucional**. Você só precisa digitar o que vem antes do '@' do seu email.

<center>
    <img src="imagens/ood_firefox.png" alt="Open on Demand @ firefox"  width="85%"/>
</center>

Se tudo der certo, você verá a tela de _login_ abaixo:

<center>
    <img src="imagens/ood_loggedin.png" alt="Open on Demand logged in"  width="85%"/>
</center>

### IMPORTANTE

Depois de fazer o primeiro login, você poderá ver e gravar arquivos na aba `Files` do Open OnDemand (ood), mas ainda não conseguirá criar jobs ou usar os `Interactive Apps`. Essa autorização é feita manualmente, então, se precisar, envie um email para um dos mantenedores (ou chame via TEAMS).

Após este primeiro login você já está apto a ver e gravar arquivos na aba `Files` do Open OnDemand (ood), mas ainda não vai conseguir criar jobs ou usar o `Interactive Apps`.

Por hora esta autorização é feita manualmente, então assim que precisar mande um email para um destes endereços (ou chame via TEAMS)

**ATENÇÃO: DEPOIS DO PRIMEIRO ACESSO, É POSSÍVEL ACESSAR O HPC MARVIN EXCLUSIVAMENTE PELO NAVEGADOR!**

### Vídeo Resumo

<figure class="video_container">
  <video controls="true" allowfullscreen="true" poster="videos/thumb_1st.png" width="852" height="480">
    <source src="videos/1stlogin.mp4" type="video/mp4">
  </video>
</figure>

<!-- ## Configuração do Ambiente de Trabalho

Após conectar-se ao HPC Marvin, você precisará configurar seu ambiente de trabalho. Isso inclui a instalação de softwares adicionais que você possa precisar para sua pesquisa e a configuração de variáveis de ambiente. Para configurar seu ambiente de trabalho, siga as instruções fornecidas abaixo:

1. Instale os softwares necessários para sua pesquisa
2. Defina as variáveis de ambiente necessárias, como $PATH, $LD_LIBRARY_PATH, etc. -->
