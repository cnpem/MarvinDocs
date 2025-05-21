# Cancelamento de jobs

Para cancelar um _job_ específico, use o comando `scancel` seguido do ID do _job_:

```bash
scancel <jon_id>
```

<div class="warning">
  <br>Substitua <code>&lt;job_id&gt;</code> pelo ID do seu <i>job</i>.<br>
</div>

Para cancelar todos os seus _jobs_ em execução ou na fila, use o seguinte comando:

```bash
scancel -u $USER
```

Sempre verifique o status do seus _jobs_ antes de cancelá-los.
