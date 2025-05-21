# Boas práticas

Para garantir o uso eficiente do sistema e evitar problemas durante a execução de _jobs_, siga estas boas práticas:

- **Especifique os recursos necessários:** Solicite apenas o que for necessário para evitar desperdício e facilitar o agendamento.

- **Defina um tempo limite adequado:** Um tempo muito curto pode interromper seu job; muito longo pode atrasar a fila.

- **Utilize o arquivo de saída:** Monitore a execução do job e facilite a depuração de erros.

- **Faça testes com jobs menores:** Teste seu pipeline com dados ou tempos reduzidos antes de escalar para execuções maiores.

- **Evite sobrecarga de I/O:** Reduza o número de acessos simultâneos ao sistema de arquivos compartilhado sempre que possível.
