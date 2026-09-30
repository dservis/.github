## Resumo
<!-- 1 a 3 linhas. O PORQUÊ da mudança. O diff já mostra o quê. -->

## Issue relacionada
<!-- Closes #123  (fecha ao mergear)  ·  Refs #123  (apenas referencia) -->
Closes #

## Tipo de mudança
<!-- Marque apenas o que se aplica. -->
- [ ] 🐛 Correção de bug
- [ ] ✨ Nova funcionalidade
- [ ] 🛠️ Refatoração / dívida técnica (sem mudança de comportamento)
- [ ] ⚙️ Configuração / infraestrutura / CI
- [ ] 📝 Documentação
- [ ] ⬆️ Atualização de dependência

## O que mudou
<!-- Lista objetiva das mudanças relevantes. Não repita o diff arquivo a arquivo. -->
-

## Como testar
<!-- Passos que o revisor consegue repetir: rota, tela, comando ou cenário. -->
1.

## Evidência
<!-- Saída de testes, logs, print ou gravação. Para API, inclua request e response. -->

## Impacto
<!-- Marque o que se aplica. Cada item marcado exige detalhe na seção "Notas de deploy". -->
- [ ] **Breaking change** — consumidores existentes precisam mudar
- [ ] Altera contrato de API (request/response)
- [ ] Altera schema de banco de dados / exige migração
- [ ] Altera permissões ou autorização
- [ ] Exige nova configuração, variável de ambiente ou segredo
- [ ] Nenhum dos anteriores

## Notas de deploy e rollback
<!-- Ordem de aplicação, migração, flags, janela. Como desfazer se der errado.
     Se marcou algum impacto acima e deixar vazio, o PR não está pronto. -->

## Checklist do autor
- [ ] O PR tem um único propósito e tamanho revisável
- [ ] Testes cobrem o caminho principal e pelo menos um caso de erro
- [ ] CI está verde, sem novos avisos
- [ ] Não há segredo, token, certificado, `.env` ou binário no diff
- [ ] Mensagens de erro e textos ao usuário seguem o padrão do projeto
- [ ] Documentação e README atualizados, se o comportamento mudou
- [ ] Fiz uma revisão do meu próprio diff antes de pedir revisão
