# 🚀 Deploy no Netlify - Pokémon Adventures

## Opção 1: Deploy Automático via GitHub (RECOMENDADO)

### Pré-requisitos
- Conta no [netlify.com](https://netlify.com) (gratuita)
- Repo privado no GitHub ✅

### Passos

1. **Tornar repo privado no GitHub:**
   - Vá em: https://github.com/giugiu-a11y/pokemon-adventures
   - Settings → Danger Zone → Change repository visibility → Private

2. **Conectar ao Netlify:**
   - Acesse https://app.netlify.com
   - Clique "Add new site" → "Import an existing project"
   - Escolha "Deploy with GitHub"
   - Autorize o Netlify no GitHub
   - Selecione o repo `pokemon-adventures`

3. **Configurar deploy:**
   ```
   Branch to deploy: main
   Build command: (deixar vazio)
   Publish directory: .
   ```
   → O `netlify.toml` já configura isso automaticamente!

4. **Clicar "Deploy site"**
   → Pronto! Site público, repo privado. 🎉

---

## Opção 2: Deploy Manual (Drag & Drop)

Sem precisar conectar GitHub:

1. Acesse https://app.netlify.com/drop
2. Arraste a pasta `pokemon-adventures-clean/` inteira
3. Aguarde o upload (a ROM tem 16MB, pode demorar)
4. Pronto! URL gerada automaticamente

⚠️ **Nota:** Deploy manual não atualiza automaticamente quando você fizer push no GitHub. Use a Opção 1 para deploys automáticos.

---

## Opção 3: Deploy via CLI (para automação futura)

### Instalar Netlify CLI
```bash
npm install -g netlify-cli
```

### Autenticar
```bash
netlify login
# Abre navegador para OAuth
```

### Obter NETLIFY_AUTH_TOKEN (para automação headless)
1. Acesse https://app.netlify.com/user/applications
2. Clique "New access token"
3. Copie o token
4. Salve em `~/.config/secrets.env`:
   ```
   NETLIFY_AUTH_TOKEN=seu_token_aqui
   ```

### Deploy
```bash
cd /home/ubuntu/clawd/pokemon-adventures-clean

# Primeiro deploy (cria novo site)
netlify deploy --dir=. --prod

# Deploys subsequentes (se já tiver site vinculado)
netlify deploy --dir=. --prod --auth=$NETLIFY_AUTH_TOKEN
```

---

## Estrutura do Projeto

```
pokemon-adventures-clean/
├── index.html          # App principal (EmulatorJS)
├── netlify.toml        # Config Netlify ✅ (criado)
├── pokefirered.gba     # ROM (16MB) - raiz
├── roms/
│   ├── firered.gba     # ROM (16MB) - usada pelo emulador
│   └── pokefirered.gba # ROM duplicata
├── saves/              # Diretório para saves
└── status.html         # Página de status
```

## Notas Importantes

- **ROM size:** 16MB por ROM, ~48MB total. Netlify permite até 100MB por deploy.
- **CDN:** EmulatorJS é carregado de `cdn.emulatorjs.org` - sem custo de banda no Netlify.
- **Saves:** Saves ficam no localStorage do navegador (não no servidor).
- **URL customizada:** No Netlify free tier, URL será `[nome-aleatorio].netlify.app`.
  Pode customizar para `pokemon-adventures.netlify.app` nas configurações de domínio.

## Após o Deploy

1. Testar: Acessar a URL gerada
2. Verificar que o emulador carrega
3. Verificar que a ROM carrega (`./roms/firered.gba`)
4. Opcional: Configurar domínio customizado

---

*Preparado por ClawdBot em 2026-02-18*
