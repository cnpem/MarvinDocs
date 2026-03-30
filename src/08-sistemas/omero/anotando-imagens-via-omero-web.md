# Anotando imagens via OMERO.web

No OMERO.web, é possível executar scripts para realizar diversas tarefas, como gestão de anotação e exportação de dados. Para acessar o menu de scripts, clique no ícone de engrenagens no canto superior direito da interface, ao lado da barra de busca.

<center>
    <img src="imagens/scripts/scripts-01.png" alt="Scripts menu"  width="70%"/>
</center>

Os scripts estão organizados por categorias, sendo que os scripts voltados à manipulação de metadados estão localizados em `annotation_scripts`.

> [!TIP]
> Selecione o objeto alvo (`Project`, `Dataset`, `Screen`, `Plate`, `Well`, `Image`) na árvore de dados antes de abrir o script. Isso fará com que os campos `Data Type` e `ID` sejam preenchidos automaticamente.

## Por que anotar as imagens?

A anotação rigorosa é essencial para a rastreabilidade científica. Metadados estruturados (*Tags*, pares *Key-Value*, comentários e anexos) são fundamentais para fluxos de análise automatizados e para a criação de conjuntos de dados alinhados aos princípios [FAIR](https://www.go-fair.org/fair-principles/) (*Findable*, *Accessible*, *Interoperable* and *Reusable*).

## *Expand Metadata*: copiar anotações para objetos filhos

O script `annotation_scripts > Expand Metadata` automatiza a cópia de anotações de um objeto para seus "filhos" na hierarquia (ex: de um Projeto para todos os seus Datasets e Imagens).

Por exemplo, em invés de anotar manualmente a tag `Tratamento` em centenas de imagens, é possível anotar apenas o `Screen` de origem e utilizar o script para replicar a tag em todos os objetos (`Plate`, `Well`, `Image`) nele contido.

**Parâmetros**:

- `Data Type`: O tipo de objeto selecionado como origem (`Project`, `Dataset`, `Screen`, `Plate`).
- `ID`: Identificador(es) do objeto. Para múltiplos alvos, separe os IDs por vírgula.
- `Annotation Type`: Tipo de metadado a ser copiado (`Tags`, `Key-Value`, `File`, `Comment` ou `All`).
- `Source Level`: Define em qual nível hierárquico o script deve buscar as anotações originais.

No exemplo abaixo, as tags de um objeto do tipo *Screen* (`ID 1953`) serão copiadas para seus objetos vinculados (*Plate*, *Well* e *Image*).

<center>
    <img src="imagens/scripts/expand_metadata-01.png" alt="Expand_Metadata.py"  width="70%"/>
</center>

No exemplo seguinte, as tags dos *Wells* pertencentes ao *Plate* com `ID 14220` seriam copiadas para os *Images* correspondentes aos *Wells* do *Plate* selecionado.

<center>
    <img src="imagens/scripts/expand_metadata-02.png" alt="Expand_Metadata.py"  width="70%"/>
</center>

## *Clean Metadata*: remover anotações

O script `annotation_scripts > Clean Metadata` a exclusão rápida e controlada de anotações, facilitando a correção de erros ou a padronização de grandes volumes de dados. Além de limpar os metadados de um objeto alvo, é possível deletar também as anotações de todos os objetos vinculados.

**Parâmetros**:

- `Data Type`: O tipo de objeto selecionado como origem (`Project`, `Dataset`, `Screen`, `Plate`).
- `ID`: Identificador(es) do objeto. Para múltiplos alvos, separe os IDs por vírgula.
- `Annotation Type`: Tipo de metadado a ser copiado (`Tags`, `Key-Value`, `File`, `Comment` ou `All`).
- `Include Children`: Se marcado, a limpeza será aplicada também a todos os objetos vinculados ao alvo selecionado.

No exemplo abaixo, as tags de um objeto do tipo *Screen* (`ID 1953`) seriam removidas, sem afetar seus objetos vinculados (*Plates*, *Wells* e *Images*).

<center>
    <img src="imagens/scripts/clean_metadata-01.png" alt="Clean_Metadata.py"  width="70%"/>
</center>

No exemplo seguinte, todas as anotações do *Plate* com `ID 14220` seriam removidas. Como a opção de `Include Children` está ativada, as anotações dos *Wells* e *Images* associados também seriam excluídas.

<center>
    <img src="imagens/scripts/clean_metadata-02.png" alt="Clean_Metadata.py"  width="70%"/>
</center>

## Boas práticas de anotação (FAIR no OMERO)

Para garantir que seus dados sejam [FAIR](https://www.go-fair.org/fair-principles/) (*Findable*, *Accessible*, *Interoperable* and *Reusable*), siga estas recomendações ao anotar imagens no OMERO:

- **Seja consistente:** utilize sempre os mesmos nomes para tags e pares key-value ao longo do projeto.
- **Use vocabulários controlados:** prefira termos padronizados (ex.: nomes de linhagens celulares, compostos, condições experimentais).
- **Inclua metadados essenciais:** anote informações críticas como linhagem celular, tratamento, tempo de exposição, tipo de microscopia, etc.
- **Evite duplicações:** antes de criar novas *tags*, verifique se elas já existem no OMERO utilizando a barra de busca.
