# Primeiro login

Para ativar seu usuário no sistema do nosso HPC (high performance computing) é preciso, fazer um primeiro acesso via terminal no `ssh` (Secury SHell).

Nos tutoriais utilizaremos o <> para indicar variáveis.
Sempre que aparecer algo entre <>, subistitua pelo valor adequado, (sem digitar o <>).

Exemplo:
Se você é a Manya Salomee Sklodowska e seu usuário é marie.curie, ao ver `<seu.login.cnpem>@lnbio.cnmpem.br`, digite `marie.curie@lnbio.cnmpem.br` para executar.


## 1. Fazendo o primeiro acesso

### Abra o seu aplicativo de terminal
No Windows abra o PowerShell <img src="fig/powershell_icon.png" alt="PowerShell logo"  width="2%"/><br>
No Linux ou MacOS abra o terminal <img src="fig/terminal_icon.png" alt="Terminal logo"  width="2.3%"/><br>

Nele vamos usar o `ssh` para acessar o *cluster*, então digite o seguinte comando:<br>
```
ssh <seu.login.cnpem>@hpc-lnbio.cnpem.br
```

Caso esteja no Windows, pode ser que apareça o seguinte erro:
<center>
  <img src="fig/powershell_no_ssh_error.png" alt="PowerShell Error"  width="80%"/><br>
</center>

Se ocorrer tente outro computador ou peça para o **tic** instalar o **ssh** na máquina que você está usuando.

Continuando, digite a sua senha **institucional** quando solicitada.
(Atenção dependendo to seu terminal, é possível que ao digitar a senha, por segurança, nada apareça na tela, nem mesmo os *s. Fique tranquilo, isso é normal. Se errar tente novamente.)

É possível que um aviso com os dizeres semelhantes aos abaixo apareça
```
[...] Are you sure you want to continue connecting (yes/no/[fingerprint])?
```
Digite `yes` e aperte **enter**

Se tudo ocorreu bem, você verá o cursor piscando no terminal com dizeres similares ao seguinte:

```
[<seu.login.cnpem>@marvin ~]$
```

* Marvin é o nome temporário de nosso HPC  <img src="fig/marvin.png" alt="Marvin bit art"  width="3%"/>.

(Se você der o comando `ls` (comando para listar o que existe no diretório), verá que já está criada uma pasta chamada `ondemand`. Verifique por favor...)

## 2. Acessando no navegador

Agora vamos ao seu navegador <img src="fig/browser_icons.png" alt="Main Browsers"  width="10%"/>

Na barra de endereços entre no seguinte site

```
https://hpc-lnbio.cnpem.br
```
Lembre-se, este site só estará disponível na rede interna, se você estiver em casa é preciso usar a **VPN**. Caso não tenha este acesso à VPN, favor solicitar à **TIC**.

No site acessado, mais uma vez, será preciso logar com o sua **senha institucional**.</br>
(Não é preciso colocar o email completo, o que vem antes do @ é o suficiente)
<center>
    <img src="fig/ood_firefox.png" alt="Open on Demand @ firefox"  width="85%"/>
</center>

Se tudo der certo você verá a tela abaixo:

<center>
    <img src="fig/ood_loggedin.png" alt="Open on Demand logged in"  width="85%"/>
</center>

### IMPORTANTE
Após este primeiro login você já está apto a ver e gravar arquivos na aba `Files` do Open OnDemand (ood), mas ainda não vai conseguir criar jobs ou usar o `Interactive Apps`.

Por hora esta autorização é feita manualmente, então assim que precisar mande um email para um destes endereços (ou chame via TEAMS)

### ATENÇÃO, DEPOIS DE FEITO O PRIMEIRO LOGIN, SE QUISER É POSSÍVE USAR APENAS VIA NAVEGADOR!

## Vídeo Resumo
<p align='center'>
    (vou regravar em FullHD, mas por enquanto vou deixar aqui para receber feedbacks sobre o formato)
</p>

<figure class="video_container">
  <video controls="true" allowfullscreen="true" poster="media/thumb_1st.png" width="852" height="480">
    <source src="media/1stlogin.mp4" type="video/mp4">
  </video>
</figure>

