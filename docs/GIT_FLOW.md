# Git Flow

## Branches permanentes

- `main`: produção. Não recebe implementação direta.
- `dev`: integração. Não pode ser excluída e recebe features por pull request.

Embora a especificação inicial mencione `develop`, a convenção vigente definida
pelo responsável é `dev`.

## Implementação

Toda alteração parte da versão atualizada de `dev`:

```bash
git switch dev
git pull --ff-only origin dev
git switch -c feature/nome-da-entrega
```

O destino do PR é sempre `dev`. Após o merge:

1. a automação exclui somente a branch `feature/*` integrada;
2. a automação abre ou atualiza o fluxo de PR de `dev` para `main`;
3. o PR permanece bloqueado até a aprovação de `@wellbenicio` e dos checks.

O merge automático em `main` não é permitido. A automação abre o PR, mas nunca
substitui a revisão humana.

## Proteções obrigatórias

`main` e `dev` exigem:

- pull request;
- aprovação do CODEOWNER `@wellbenicio`;
- nova aprovação quando houver alterações após a revisão;
- conversas resolvidas;
- branch atualizada;
- checks obrigatórios aprovados;
- proibição de force push e exclusão.

O Quality Gate do Sonar será adicionado aos checks obrigatórios assim que o
projeto de análise for criado durante o bootstrap da aplicação.
