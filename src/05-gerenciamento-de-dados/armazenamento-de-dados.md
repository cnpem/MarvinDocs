# Armazenamento de dados

O HPCC Marvin fornece duas opções principais de armazenamento de dados: pasta pessoal e pasta compartilhada por grupos de pesquisa.

## Pasta pessoal

Cada usuário do HPCC Marvin tem acesso a um espaço de armazenamento pessoal, onde pode armazenar e compartilhar seus dados. 

<div class="warning">
Se você é a Marie Skłodowska-Curie e seu usuário é <code>marie.curie</code>, sua pasta estará localizado em <code>/home/marie.curie</code>. Você acessa sua pasta pessoal ao fazer login no sistema, e ela é automaticamente montada como seu diretório inicial (<code>$HOME</code>).
</div>

Esta pasta (e.g., seu `HOME`) é exclusiva para cada usuário e é utilizado para guardar arquivos, scripts, resultados e dados intermediários necessários apenas para suas atividades de pesquisa.

## Pasta compartilhada por grupos de pesquisa

Os grupos de pesquisa podem solicitar uma pasta compartilhada para armazenar dados que precisam ser acessados por vários membros do grupo.

<div class="warning">
Esta pasta é criada em um diretório específico, como <code>/shared/groups/&lt;sigla-do-grupo&gt;</code>.
</div>

Para solicitar uma pasta compartilhada, entre em contato com a equipe do EDB através do e-mail <a href="mailto:edb@lnbio.cnpem.br">edb@lnbio.cnpem.br</a> com o assunto "[Marvin] Pasta compartilhada". Informe o nome do grupo de pesquisa e a sigla que deseja (`/shared/groups/<sigla-do-grupo>`).

<div class="warning">
Após a criação da pasta, o solicitante deverá compartilhar a pasta com os demais membros do grupo. Para mais informações sobre como compartilhar o acesso a essa pasta compartilhada, consulte a seção de 
<a href="compartilhamento-de-dados.md">Compartilhamento de dados</a>.
</div>
