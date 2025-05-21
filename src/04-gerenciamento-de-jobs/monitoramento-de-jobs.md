# Monitoramento de jobs

Para acompanhar o status dos seus _jobs_, você pode usar o comando `squeue`:

```bash
squeue -u $USER
```

Para obter informações detalhadas de um job específico, use o comando `scontrol`:

```bash
scontrol show job <job_id>  
```

<div class="warning">
  <br>Substitua <code>&lt;job_id&gt;</code> pelo ID do seu <i>job</i>.<br>
</div>
