# Deploy PuterAI Gateway pe Docker / Easypanel

## Local Docker

```bash
docker compose up -d --build
```

Deschide:

- `http://localhost:8000/bridge`
- `http://localhost:8000/chat`
- `http://localhost:8000/docs`

Important: bridge-ul trebuie ținut deschis într-un browser unde ești logat în Puter.

## Easypanel

### Variantă recomandată: Git Repository

1. Easypanel → `Create Project`
2. `Create Service` → `App`
3. Source → `GitHub Repository`
4. Repo: `https://github.com/Mr-DS-ML-85/PuterAI-Gateway`
5. Build type → `Dockerfile`
6. Port → `8000`
7. Env:
   ```env
   PORT=8000
   ```
8. Deploy.

După deploy:

- `https://domeniul-tau/bridge`
- `https://domeniul-tau/chat`
- `https://domeniul-tau/docs`
- `https://domeniul-tau/v1`

## Test API

```bash
curl https://domeniul-tau/health
```

Apoi deschide `https://domeniul-tau/bridge`, autentifică Puter, ține tab-ul deschis.

Exemplu OpenAI SDK:

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://domeniul-tau/v1",
    api_key="no-key-needed"
)

r = client.chat.completions.create(
    model="claude-opus-4-7",
    messages=[{"role": "user", "content": "Salut!"}]
)

print(r.choices[0].message.content)
```

## Atenție

Serverul Docker/Easypanel nu poate apela Puter singur. Modelul rulează prin `bridge.html` în browserul tău autentificat Puter. Fără bridge deschis → API returnează `503 Bridge not connected`.