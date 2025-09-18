# Gerenciamento de ambiente

O HPCC Marvin oferece flexibilidade para que os usuários configurem seus próprios ambientes de desenvolvimento. O gerenciamento de ambientes é feito por meio do **sistema de módulos (Lmod)**, o que permite carregar, combinar e personalizar bibliotecas conforme as necessidades de cada projeto.

Para visualizar os módulos disponíveis, utilize:

```bash
module avail
```

Para carregar um módulo específico, use:

```bash
module load <nome>/<versão>
```

<div class="warning">
    <br>Quando múltiplas versões de um software estão disponíveis, uma delas é definida como padrão (indicada por <code>(D)</code>).<br>
</div>

Para listar os módulos atualmente carregados:

```bash
module list
```

## Ambiente de desenvolvimento

Além dos módulos pré-instalados, os usuários podem criar e gerenciar seus próprios ambientes com ferramentas como:

- [miniforge](https://conda-forge.org/): Ambiente e gerenciamento de pacotes para Python, R, C/C++ e outras linguagens. Para habilitar, carregue o módulo `miniforge`:
  
```bash
module load miniforge
```

- [uv](https://docs.astral.sh/uv/): Gerenciador de ambientes Python extremamente rápido e leve, compatível com `pip` e `pyproject.toml`. Para habilitar, carregue o módulo `uv`:
  
```bash
module load uv
```

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

- Criar ambientes virtuais reutilizáveis com `uv` e `miniforge`;
- Manter os ambientes organizados, evitando a criação de múltiplos ambientes redundantes;
- Documentar dependências em arquivos como `README.md`, `pyproject.toml` (`uv`/`pip`), `requirements.txt` (`uv`/`pip`) e/ou `environment.yml` (`conda`/`mamba`), facilitando o compartilhamento e a reprodução do ambiente por outros usuários.
