# treino-dev

PWA de acompanhamento de um plano de estudos de 25 dias para entrevista técnica:
algoritmos, live coding, JavaScript, Web e Backend.

Estático, sem build e sem dependência. Funciona offline depois da primeira abertura e pode ser
instalado no Android e no desktop.

```
index.html              o app inteiro (HTML + CSS + JS num arquivo só)
manifest.webmanifest    nome, ícones, cor e modo standalone
sw.js                   service worker: cache offline
icons/                  ícones 192, 512 e maskable
```

## Funcionalidades

- Trilha de 25 dias, abrindo direto no dia atual
- Exercícios do dia com link para LeetCode e documentação
- Cronômetro para simulados e live coding (45, 60, 75 min)
- Anotações por dia, salvas automaticamente
- Checklist de conhecimentos (Algoritmos, JavaScript, Web, Backend)
- Progresso no `localStorage`, com exportar/importar em JSON
- Tema claro e escuro

## Publicar

**Service worker só funciona em HTTPS** (ou em `localhost`). Abrir o `index.html` com duplo
clique — `file://` — não registra o SW e não instala.

### GitHub Pages

Settings → Pages → Source: `Deploy from a branch`, branch `main`, pasta `/ (root)`.
Sai em `https://devgusta5.github.io/treino-dev/`.

### Vercel

```bash
npx vercel --prod
```

Sem framework e sem build — site estático.

### Rodar local

```bash
npx serve .          # ou: python3 -m http.server 8080
```

Abra `http://localhost:8080` — em localhost o service worker registra normalmente.

## Instalar

- **Android/Chrome:** botão **Instalar app** no rodapé, ou menu ⋮ → *Instalar aplicativo*.
- **Desktop (Chrome/Edge):** ícone de instalar na barra de endereço.
- **iOS/Safari:** Compartilhar → *Adicionar à Tela de Início* (o iOS ignora o prompt automático).

## Progresso

Fica no `localStorage`, por dispositivo — não sincroniza sozinho entre celular e PC. Use
**Exportar progresso** / **Importar progresso** no rodapé para passar de um para o outro.
Limpar os dados do site apaga o progresso.

## Editar o conteúdo

Tudo mora no `index.html`:

- `const DIAS = [...]` — os 25 dias: título, objetivo, capítulo do livro, exercícios (`ex`) e
  perguntas (`qs`). `s:"lc"` marca link do LeetCode, `s:"doc"` leitura, `s:"task"` tarefa sem link.
- `kind:"sim"` marca dia de avaliação, `kind:"rest"` descanso, `timer: 60` liga o cronômetro.
- `CHECKLIST` e `RECURSOS` — as outras duas abas.

Depois de editar, **incremente `VERSION` no `sw.js`** (`v1` → `v2`) e publique de novo. Sem isso
o navegador continua servindo a versão antiga do cache.
