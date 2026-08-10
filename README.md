# QC Quadros Elétricos — Sidel (MOD_105_IE_SMF_02)

Aplicação de checklist de verificação de quadros elétricos.
Funciona no **PC** (qualquer navegador) e no **telemóvel** (app instalável, offline).
Publica-se gratuitamente no **GitHub Pages**.

- Checklist **MOD_105_IE_SMF_02** — 45 pontos, 7 secções.
- **Fase 1** (1.1 → 6.2): montagem e pré-testes. **Fase 2** (6.3 → 7.5): testes finais e aprovação.
- Validação sequencial, fotos ou documentos, relatório em PDF (impressão), utilizador no fim.
- Dados guardados no dispositivo (offline). Controlo de versões no menu «Sobre».

## Ficheiros (é isto que vai para o GitHub)
```
index.html              a aplicação (PC + telemóvel)
firebase-config.js      configuração da sincronização na nuvem (opcional)
manifest.webmanifest    metadados da app instalável
sw.js                   funcionamento offline
icon-192.png            ícone
icon-512.png            ícone
README.md               este ficheiro
```

## Sincronização na nuvem (editar no PC e no telemóvel)
Por defeito os dados ficam **no dispositivo**. Para veres e editares os mesmos
relatórios em qualquer dispositivo, ativa o Firebase (gratuito):

1. Vai a https://console.firebase.google.com → **Adicionar projeto** (dá um nome, avança).
2. **Compilação → Firestore Database → Criar base de dados** → modo de produção → região Europa.
3. **Compilação → Authentication → Começar →** ativa **Email/palavra-passe**.
4. **Definições do projeto** (⚙) → **Os teus apps** → ícone **Web `</>`** → regista a app →
   copia o objeto `firebaseConfig` e cola-o no ficheiro **`firebase-config.js`**.
5. Em **Firestore → Regras**, cola isto e publica:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /inspecoes/{id} {
         allow read, write: if request.auth != null;
         match /anexos/{aid} { allow read, write: if request.auth != null; }
       }
     }
   }
   ```
6. Faz commit/upload dos ficheiros para o GitHub.
7. Na app: menu **Sincronização → Criar conta** (uma vez). Depois entra com a
   **mesma conta** no PC e no telemóvel — os relatórios passam a sincronizar
   automaticamente (e funcionam offline, enviando quando houver ligação).

> Todos os que entrarem com uma conta do teu projeto veem e editam os mesmos
> relatórios (ideal para uma equipa). Sem configurar o Firebase, a app continua
> a funcionar normalmente, só que local a cada dispositivo.

## Usar no PC
- Rápido: duplo-clique no `index.html` — abre no navegador e funciona.
- Ou abre o link publicado (ver abaixo) em Chrome/Edge. Em Chrome/Edge podes clicar
  no ícone «Instalar» na barra de endereço para a teres como janela de app.

## Publicar no GitHub Pages (para usar no telemóvel)
### Pelo site (sem instalar nada)
1. Cria conta em https://github.com → **New repository**.
2. Nome, por ex.: `qc-quadros` · **Public** · **Create**.
3. **Add file → Upload files** → arrasta **todos** os ficheiros desta pasta → **Commit changes**.
4. **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main` / `/(root)` → **Save**.
5. Ao fim de ~1 min a app fica em:
   `https://SEU_UTILIZADOR.github.io/qc-quadros/`

### Por Git (linha de comandos)
```bash
git init
git add .
git commit -m "QC Quadros MOD_105_IE_SMF_02"
git branch -M main
git remote add origin https://github.com/SEU_UTILIZADOR/qc-quadros.git
git push -u origin main
```

## Instalar no telemóvel
1. Abre o link `https://SEU_UTILIZADOR.github.io/qc-quadros/`.
2. **Android/Chrome:** menu ⋮ → **Adicionar ao ecrã principal**.
   **iPhone/Safari:** Partilhar → **Adicionar ao ecrã principal**.
3. Fica com ícone de app e funciona offline.

> O modo instalável/offline exige **https** (o GitHub Pages já é https). Aberta por
> duplo-clique no PC funciona na mesma, sem o «instalar».

## Controlo de versões
Versão atual: **MOD_105_IE_SMF_02** (30/07/2026). Para novas versões, edita as
constantes `DOC_VER` e `DOC_HIST` no topo do `<script>` em `index.html`.
