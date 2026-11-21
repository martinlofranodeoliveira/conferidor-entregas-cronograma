# Conferidor de Entregas por Cronograma

Confira entregas parciais por item, unidades pendentes e registros recebidos após o prazo previsto.

## Como usar

Abra a [demonstração](https://martinlofranodeoliveira.github.io/conferidor-entregas-cronograma/). Para uso local, execute `python3 -m http.server 8000` no diretório e abra `http://localhost:8000`.

Informe asOf, schedule com id, expected e dueDate, e deliveries com id, quantity e receivedOn.

## Contrato público

Datas são strings ASCII no formato YYYY-MM-DD de 2000-01-01 a 2100-12-31, sem hora nem fuso. Valide o calendário gregoriano incluindo fevereiro e anos bissextos. Um dia tem 24 horas neste cálculo. Use datas explícitas da entrada, sem consultar o relógio. input é objeto com asOf (data), schedule (array de até 100 {id,expected,dueDate}) e deliveries (até 200 {id,quantity,receivedOn}). id tem 1 a 32 caracteres ASCII alfanuméricos, hífen ou sublinhado. id é único em schedule. Cada delivery aponta a um id do cronograma, admite repetição e não pode ocorrer após asOf. expected e quantity são inteiros de 1 a 1000000. Entrada inválida retorna exatamente {error:"INVALID_INPUT"}.
Retorne {rows,summary}. rows, na ordem de schedule, reúne {id,received,pending,excess,lateEntries,overdue,status}. received é a soma das entregas daquele id; pending=max(0,expected-received), excess=max(0,received-expected), lateEntries é contagem de entregas daquele id com receivedOn depois de dueDate; overdue marca pending>0 e dueDate estritamente antes de asOf. status é PENDING se received=0, PARTIAL se 0<received<expected, COMPLETE se igual, EXTRA se acima. summary tem pendingItems, overdueItems, lateEntries e excessItems com as contagens.

## Escopo

Demonstração offline com exemplos fictícios. A equipe responsável avalia documentação, conformidade e habilitação. A interface processa os dados no navegador. O motor foi gerado com Gemini 4 Neon no Vertex AI.

## Testes

Execute `node scripts/test.mjs public.json`.

## Licença

MIT. Acorn preserva sua licença em scripts/vendor/LICENSE-Acorn.txt.
