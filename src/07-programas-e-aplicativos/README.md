# Aplicativos e Programas

No HPCC Marvin, os aplicativos e programas são disponibilizados principalmente por meio do **sistema de módulos (Lmod)**, permitindo que os usuários carreguem e utilizem diferentes versões conforme suas necessidades. Eventualmente, alguns podem estar disponíveis fora deste padrão, quando há necessidades específicas ou limitações técnicas.

Para listar os módulos disponíveis, utilize o comando:

```bash
module avail
```

Para listar os módulos com a descrição, utilize:

```bash
module spider
```

Para carregar um módulo específico, use:

```bash
module load <nome>/<versão>
```

<div class="warning">
    <br>Quando múltiplas versões de um software estão disponíveis, uma delas é definida como padrão (indicada por <code>(D)</code>).<br>
</div>

Para listar os módulos carregados na sua sessão, utilize:

```bash
module list
```

Para solicitar a instalação ou atualização de um aplicativo ou programa, registre um chamado <a href="https://cnpem.atlassian.net/servicedesk/customer/portal/181" target="_blank">[LNBio] Suporte EDB</a> do Jira em <a href="https://cnpem.atlassian.net/servicedesk/customer/portal/181/group/536/create/2154" target="_blank">HPCC Marvin: Aplicativos, Programas e Sistemas</a>.

---

## Bioimagens

Os programas e aplicativos relacionados à processamento e análise de imagens biológicas são:

- [Cellpose](./cellpose/index.html)
- [CellProfiler](./cellprofiler/index.html)
- [Fiji](./fiji/index.html)
- [Ilastik](./ilastik/index.html)

## Biologia Estrutural

Os programas e aplicativos relacionados à modelagem, predição e análise estrutural de proteínas são:

- [AlphaFold](./alphafold/index.html)

## Descoberta de fármacos (_Drug Discovery_)

Os programas e aplicativos relacionados à descoberta e desenvolvimento de fármacos são:

- [NP³ MS WORKFLOW](./np3_ms_workflow/index.html)
<!-- - [NP³ Blob Label](./np3_blob_label/index.html) -->

---
