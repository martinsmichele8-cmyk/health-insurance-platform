# Sistema da Seguradora

SaaS de operações para seguradoras, com uma visão unificada de carteira, apólices, sinistros, subscrição e risco.

## Produto

O sistema apoia equipes de operações e análise em decisões diárias:

- visão executiva da carteira e dos indicadores de risco;
- consulta e cadastro de apólices;
- triagem e registro de sinistros;
- fila de subscrição com score e recomendação;
- estados claros de carregamento, vazio e erro.

## Arquitetura

- `artifacts/seguradora-dashboard`: frontend React + Vite;
- `artifacts/api-server`: API Express;
- `lib/api-spec`: contrato OpenAPI;
- `lib/api-client-react`: hooks React Query gerados;
- `lib/api-zod`: validações Zod geradas;
- `lib/db`: schema Drizzle para PostgreSQL.

## Desenvolvimento

Requisitos: Node.js 22+ e pnpm.

```bash
cp .env.example .env
pnpm install
pnpm run typecheck:libs
pnpm --filter @workspace/api-server run typecheck
pnpm --filter @workspace/seguradora-dashboard run dev
```

O frontend e a API devem ser executados em processos separados durante o desenvolvimento. Configure `DATABASE_URL` antes de iniciar a API para usar os dados persistidos.

## Segurança

Arquivos `.env` não fazem parte do repositório. Use os secrets do ambiente de execução; nunca adicione credenciais ao Git.

## Publicação

O `vercel.json` configura a compilação do frontend Vite. A API precisa ser publicada com acesso ao PostgreSQL e com `DATABASE_URL` configurada no ambiente de produção.

## CI

O workflow em `.github/workflows/ci.yml` executa instalação congelada, checagem de tipos e build do frontend em cada push e pull request.
