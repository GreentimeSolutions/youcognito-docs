# Run it locally

You need **Node 22**.

```bash
git clone https://github.com/GreentimeSolutions/template.git youcognito
cd youcognito
npm install
npm run dev          # http://localhost:8080
```

With nothing configured, the app runs on an embedded **PGLite** database and the AI, faucet and art features politely report that they aren't set up. That's enough to work on the UI.

## Useful scripts

| Command | What it does |
| --- | --- |
| `npm run dev` | Dev server on port 8080 |
| `npm run build` | Production build (outputs `.vercel/output`), then runs database migrations |
| `npm run typecheck` | TypeScript check |
| `npm run lint` | ESLint |
| `npm test` | Script and auth tests |
| `npm run test:listen` | Listen-boost rule tests |
| `npm run db:migrate` | Apply pending migrations |

## Configure features

Copy `.env.example` to `.env` and fill in only what you need. See [Configuration](configuration.md) for what each setting does.

{% hint style="danger" %}
Never commit `.env`, and never use a funded wallet's private key for local testing. Use a throwaway wallet.
{% endhint %}

## Deploy (Vercel)

1. Import the repo at vercel.com/new.
2. Framework preset **Other**; build command `npm run build` (output is generated in `.vercel/output`).
3. Add environment variables, including a Postgres `DATABASE_URL`. The faucet refuses to run on Vercel without a shared database.
4. Deploy.
