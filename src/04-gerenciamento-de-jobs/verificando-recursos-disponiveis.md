# Verificando recursos disponíveis

O SLURM fornece ferramentas para verificar a disponibilidade de recursos no cluster. Para visualizar as partições disponíveis e seus limites, você pode usar o comando:

```bash
sinfo
```

Esse comando exibe informações sobre as partições, incluindo o número de nós disponíveis, o número de nós ocupados e o estado atual de cada partição.

Para visualizar informações detalhadas sobre os nós, incluindo o estado de cada nó, você pode usar:

```bash
sinfo -N -l
```

Esse comando fornece uma visão detalhada de cada nó, incluindo informações sobre a memória, CPUs e o estado atual.
