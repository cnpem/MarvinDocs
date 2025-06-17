# Ambiente de desenvolvimento

O HPCC Marvin oferece flexibilidade para que os usuários configurem seus próprios ambientes de desenvolvimento. O **gerenciamento de ambientes é feito a nível de usuário**, permitindo que cada usuário personalize seu ambiente de acordo com as necessidades dos seus projetos.

<div class="warning"> 
⚠️ O Marvin ainda <u><b>NÃO</b></u> utiliza módulos de ambiente (como <code>Lmod</code>) para gerenciamento de ambientes e bibliotecas. Cada usuário é responsável pela criação, manutenção e ativação dos seus próprios ambientes.
</div>

## Gerenciamento de Ambientes

Os usuários podem criar e gerenciar seus próprios ambientes utilizando ferramentas como:

- [conda](https://anaconda.org/anaconda/conda): Ambiente e gerenciamento de pacotes para Python, R, C/C++ e outras linguagens.

- [uv](https://docs.astral.sh/uv/): Gerenciador de ambientes Python extremamente rápido e leve, compatível com `pip` e `pyproject.toml`.

<div class="warning">
⚠️ Ferramentas como <code>conda</code> e <code>uv</code> não estão pré-instaladas no sistema. Cada usuário deve realizar a instalação dessas ferramentas em seu ambiente pessoal ou no espaço de projeto, conforme necessário.

Para instalar o <code>conda</code>, execute:

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

Para instalar o <code>uv</code>, execute:

```bash
curl -sSL https://astral.sh/uv/install.sh | bash
```
</div>

## Compiladores

O Marvin oferece suporte para desenvolvimento de aplicações em C, C++, Fortran e outros, com os seguintes compiladores e ferramentas de build disponíveis no ambiente padrão:

| Ferramenta | Descrição                        |
| ---------- | -------------------------------- |
| `gcc`      | Compilador GNU para C            |
| `g++`      | Compilador GNU para C++          |
| `gfortran` | Compilador GNU para Fortran      |
| `clang`    | Compilador LLVM para C           |
| `clang++`  | Compilador LLVM para C++         |
| `make`     | Gerenciador de build tradicional |
| `cmake`    | Sistema de build multiplataforma |

## Boas práticas

Para garantir um ambiente de desenvolvimento eficiente e organizado, recomenda-se:

- Instale seus ambientes no seu diretório pessoal (`/home/marie.curie`) ou no seu espaço de projeto.
- Utilize ferramentas como `conda`, `mamba` ou `uv` para gerenciar dependências e ambientes virtuais.
- Mantenha seus ambientes organizados e evite acumular múltiplos ambientes desnecessários.
- Documente seus ambientes e dependências em um arquivo `README.md`, `pyproject.toml` (`uv`/`pip`), `requirements.txt` (`uv`/`pip`) e/ou `environment.yml` (`conda`/`mamba`), para facilitar o compartilhamento e a reprodução do ambiente por outros usuários.
