# AGENTS.md

Instruções para agentes de IA que trabalham neste repositório. O critério é o
mesmo de sempre, e está em [CONTRIBUTING.md](CONTRIBUTING.md): quem assina o
pull request responde pela qualidade dele. Mande o que você entende e
consegue defender — não o que saiu pronto e você não leu.

## Nada de dado pessoal entra no repositório

**Nenhum dado de quem usa o app vai para o repositório.** Nem em mensagem de
commit, nem em descrição de pull request, nem em comentário de código, teste,
exemplo, nome de arquivo ou captura de tela. O repositório é público e a base
de quem escreve o código é a base de outra pessoa.

São dado pessoal, entre outros:

- saldo, fatura, limite, valor de lançamento, orçamento, meta;
- nome de banco, nome da pessoa, login, e-mail, telefone, documento;
- host, domínio, IP, caminho do servidor de quem roda;
- descrição de transação real vinda do extrato de alguém — "Padaria X", o nome
  do estabelecimento e o valor juntos dizem de quem é a conta.

O pior lugar é a mensagem de commit e a descrição de PR, porque ficam no
histórico para sempre e ninguém lê de novo antes de dar merge. Escrever
"corrigi o saldo que estava em R$ 9.999,99" para explicar o bug entrega o
dinheiro de uma casa para o mundo.

O que escrever no lugar:

- **o efeito da mudança para quem usa**, sem número da sua base;
- "o servidor de teste" no lugar do seu host, e "a base local" no lugar de
  `/data`;
- valor de exemplo inventado e redondo, quando o exemplo ajudar;
- print com o valor tarjado, como o template de pull request já pede.

**Nunca copie linha do banco, saída de log ou resposta de API real** para
explicar um defeito. Se o defeito só se reproduz com aquele dado, reduza até
reproduzir com dado inventado — um nome de banco a menos costuma bastar. Ao
consertar base de verdade, descreva o conserto ("os lançamentos que tratavam o
cartão como conta foram apagados e reimportados"), não o resultado
("sobraram 400 linhas, faltando R$ 40").

Vale para o material de teste também: um teste que usa nome, saldo ou
estabelecimento real da sua casa é o mesmo vazamento, com a desculpa de que
"é só fixture".

## Antes de abrir o pull request

1. `git diff main` e releia a mensagem de commit procurando dado de quem usa.
   Nenhum nome, número ou valor de conta deve aparecer ali.
2. Confira `.github/pull_request_template.md` — a checklist dele já tem a
   pergunta certa: "não há dado pessoal meu no diff?".
3. `ruff`, compilação do Python, build da imagem e o teste dos anexos precisam
   passar. Detalhes em [CONTRIBUTING.md](CONTRIBUTING.md).

## Convenções em uma linha

- Código, comentário, nome de função e de rota em **português**; interface e
  documentação pública em pt-BR e inglês.
- Mensagem de commit em português, no imperativo, dizendo o efeito para quem
  usa; sem `feat:`/`fix:`.
- Mudança de schema é **migration nova** em `migrations/`; nunca edite uma
  migration já publicada.
- Nada de domínio, IP ou token fixo no código — o que variar por instalação vai
  para o `.env`, com padrão sensato e uma linha no `.env.example`.
- O que aparece na tela tem que ser verdade: rótulo que promete um indicador
  precisa mostrar aquele indicador.
- Nada de `data/` no versionado: é a base de quem roda.
