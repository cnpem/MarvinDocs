# Administração do OMERO 🛠️
https://www.java.com/pt-BR/download/help/windows_manual_download.html
O cluster Sonny é mantido pelos administradores do LBC, que trabalham constantemente para garantir seu funcionamento eficiente e sem interrupções. Nesta seção, fornecemos informações sobre a administação do cluster Sonny pelo LBC.

## Atualizações do sistema

O cluster Sonny usa o sistema operacional [openSUSE MicroOS](https://microos.opensuse.org/), que possui administração e aplicação de patches automatizadas. A rotina de atualização do sistema é diária, geralmente iniciando às 00:00. Com isso, os administradores do LBC garantem que o sistemas operacional do Sonny estejam atualizados com as últimas versões de segurança e correções de bugs.

<!-- [WIP] Durante as atualizações, é necessário que nenhum trabalho esteja sendo executado. -->

## Monitoramento de recursos

Os administradores do LBC monitoram constantemente a utilização dos recursos do Sonny, incluindo CPU, memória e armazenamento, para garantir seu funcionamento eficiente e sem problemas de desempenho. Além disso, monitoram as filas de trabalhos e a alocação de recursos.

Os serviços, Podman containers, configurações de rede e logs são monitorados via cockpit em <http://sonny.cnpem.br/cockpit>. Já o monitoramento da storage é feito via Synology em <http://sonny.cnpem.br/storage>. Para o gerenciamento e monitoramento de trabalhos, é utilizado o SLURM, por meio do comando `squeue` no terminal.

Ao monitorar constantemente os recursos do Sonny, os administradores podem identificar possíveis problemas e tomar as medidas necessárias para garantir a disponibilidade contínua do cluster.

## Instalação de programas e aplicativos

A instalação de recursos no cluster Sonny requer a permissão `sudo` ao usuário. Caso não possua essa permissão, é recomendado instalar os programas e aplicativos através do gerenciador de pacotes e ambientes, como [Anaconda](https://www.anaconda.com/), [Miniconda](https://docs.conda.io/en/latest/miniconda.html), ou [Mamba](https://mamba.readthedocs.io/en/latest/index.html). Esses gerenciadores permitem a instalação de diversas ferramentas e bibliotecas necessárias para análise de dados e programação científica.

<!-- A IDEIA É INSTALAR APLICAÇÕES VIA DOCKER CONTAINER PARA SIMPLIFICAR O FUNCIONAMENTO -->

No entanto, caso não seja possível instalar o programa ou aplicativo via gerenciador de pacotes, é necessário solicitar a instalação do pacote a um administrador do LBC, que avaliará a necessidade e segurança da instalação.

## Solução de problemas

Se você encontrar algum problema ao usar o Sonny, entre em contato com os administradores do LBC. Eles podem ajudar a solucionar problemas de desempenho, questões de configuração e outros problemas técnicos relacionados ao cluster.

Os administradores do LBC estão sempre trabalhando para garantir que o Sonny esteja funcionando da melhor maneira possível e estão disponíveis para responder a quaisquer perguntas ou preocupações que você possa ter. Entre em contato conosco se precisar de ajuda ou tiver alguma dúvida!
