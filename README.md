# Plugin Domínio – Cabeda

Auditoria e análise do ERP **Domínio** dentro do Claude (Claude Code e app desktop).

O plugin instala três coisas:

| Peça | O que faz | Onde roda |
|---|---|---|
| Skill `auditoria-dominio` | O roteiro de trabalho | No Claude |
| Ponte ODBC (`@cabeda/dominio-ponte`) | Executa consultas **somente leitura** no banco Domínio do escritório | No seu computador |
| Conector Domínio (`mcp.cabeda.com.br`) | Login, licença, mapa das tabelas e consultas prontas | Servidor da Cabeda |

Os dados do banco **não passam pela Cabeda**: a ponte devolve o resultado direto ao Claude no seu computador. Veja [PRIVACIDADE.md](PRIVACIDADE.md).

## Requisitos

- Cadastro e licença ativa do Conector Domínio: [cabeda.com.br](https://www.cabeda.com.br).
- Windows com o ERP Domínio, o driver ODBC do SQL Anywhere e um DSN configurado (padrão `Contabil`) com um usuário **somente leitura** (ex.: `EXTERNO`), com usuário e senha salvos no DSN.
- Node.js 20 ou superior.
- Claude Code ou o app desktop do Claude, em plano pago.

## Instalação no Claude Code

```text
/plugin marketplace add compucel/dominio-plugin
/plugin install dominio@cabeda
```

Se o seu DSN não se chamar `Contabil`, defina a variável de ambiente `DOMINIO_DSN` antes de abrir o Claude Code.

Na primeira chamada ao conector, o Claude abre a tela de login da Cabeda. Entre com o e-mail cadastrado.

> No Windows nativo, se a ponte não iniciar com `npx`, troque em `.mcp.json` o comando por `"command": "cmd", "args": ["/c", "npx", "-y", "@cabeda/dominio-ponte@0.1"]`.

## Exemplos de uso

1. "Valide a apuração de 09/2026 das empresas 181 e 318 e aponte inconsistências."
2. "Quais empresas tiveram movimento em 09/2026 e não foram apuradas? Compare a receita com a base do DAS."
3. "Audite os acumuladores da empresa 8 de janeiro a setembro de 2026."
4. "Há quebra de saldo credor entre agosto e setembro de 2026?"

## Segurança

- A ponte só aceita um `SELECT` por vez, só em tabelas `bethadba.*` e `sys.*`, até 5.000 linhas e 60 segundos. Detalhes em [dominio-ponte](https://github.com/compucel/dominio-ponte).
- A proteção principal é o usuário de banco somente leitura no DSN.
- Todas as ferramentas são marcadas como somente leitura.

## Suporte

adm@cabeda.com.br

## Política de privacidade

Ver [PRIVACIDADE.md](PRIVACIDADE.md).
