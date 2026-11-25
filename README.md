# Wane Queiroz | Mini site para link da bio

Site estático (só HTML e CSS, sem JavaScript) em que a página inteira é o flyer.
Áreas clicáveis invisíveis ficam por cima dos botões da imagem.

```
wane-queiroz/
  index.html
  css/style.css
  assets/img/flyer.jpg   (flyer, 941 x 1671 px)
  assets/img/logo.png    (favicon, gerado a partir do logo do flyer)
  README.md
```

## 1. Links já configurados

| Destino | Link |
|---|---|
| WhatsApp | `https://wa.me/5581995660902` (com a mensagem pronta) |
| Instagram | `https://www.instagram.com/wanequeiroz/` |

Para trocar o número ou o @ no futuro, abra o `index.html` e use "Localizar e substituir"
em `5581995660902` (WhatsApp, 3 ocorrências) e `wanequeiroz` (Instagram, 3 ocorrências).
O número vai no formato 55 + DDD + número, só dígitos.

O botão de localização (Surubim - PE) abre uma busca no Google Maps. Para apontar
para o endereço exato da clínica, abra o local no Google Maps, copie o link de
"Compartilhar" e cole no `href` da âncora `.hit--loc`.

A mensagem pronta do WhatsApp é: "Olá! Vim pelo seu Instagram e gostaria de agendar um horário."
Ela está codificada em URL no trecho `?text=...`. Para mudar, gere o texto codificado
em qualquer "URL encoder" online e cole depois de `?text=`.

## 2. Ver no computador

Opção simples: dê dois cliques no `index.html`. Ele abre no navegador.

Para testar como no celular: abra o navegador, aperte F12 e ative o modo celular
(ícone de telefone/tablet). Escolha, por exemplo, iPhone 14 Pro.

Opção com servidor local (se tiver Python instalado), dentro da pasta do site:

```
python -m http.server 8000
```

Depois acesse http://localhost:8000.

## 3. Publicar no GitHub Pages

1. Crie uma conta em github.com e um repositório novo, público (ex.: `wane-queiroz`).
2. Envie os arquivos: botão "Add file" > "Upload files", arraste o **conteúdo** da pasta
   (`index.html`, `css`, `assets`, `README.md`) e confirme em "Commit changes".
   O `index.html` precisa ficar na raiz do repositório.
3. Vá em **Settings > Pages**. Em "Build and deployment", escolha
   **Deploy from a branch**, branch `main`, pasta `/ (root)` e clique em Save.
4. Aguarde 1 a 2 minutos. O endereço será
   `https://SEU-USUARIO.github.io/wane-queiroz/`.
5. Cole esse endereço no campo "Link" do perfil do Instagram.

## 4. Publicar na Vercel

**Pelo site (sem instalar nada):**

1. Crie uma conta em vercel.com (pode entrar com o GitHub).
2. Se o site já estiver no GitHub: "Add New > Project", escolha o repositório e clique em Deploy.
   Não precisa mudar nenhuma configuração (Framework Preset: Other, sem build command).
3. Se preferir sem GitHub, instale o Node.js e rode dentro da pasta do site:

```
npx vercel
```

   Responda as perguntas com Enter, aceitando os padrões. Para publicar de verdade
   (domínio de produção), rode `npx vercel --prod`.

O endereço final será algo como `https://wane-queiroz.vercel.app`.

## 5. Editar links e posição das áreas

**Links:** no `index.html`, cada área é uma âncora `<a class="hit ...">`. Mude o `href`
e o `aria-label` (texto lido por leitores de tela).

**Posição e tamanho:** no `css/style.css`, cada área tem uma linha como:

```
.hit--wa-btn { left: 10.096%; top: 27.349%; width: 38.363%; height: 4.788%; }
```

Os valores são porcentagens da imagem. Para calcular a partir de pixels do flyer
(941 x 1671 px):

```
left   = x do canto esquerdo / 941  * 100
top    = y do canto superior / 1671 * 100
width  = largura do botão    / 941  * 100
height = altura do botão     / 1671 * 100
```

Para enxergar as áreas enquanto ajusta, adicione temporariamente no CSS:

```
.hit { outline: 2px solid lime; }
```

Remova a linha depois.

| Classe | Onde fica | Destino |
|---|---|---|
| `.hit--logo` | logo e nome no topo | Instagram |
| `.hit--wa-btn` | "Agendar seu atendimento" | WhatsApp |
| `.hit--ig-btn` | "Acompanhe meu trabalho" | Instagram |
| `.hit--cta` | "Cuide do seu sorriso hoje mesmo!" | WhatsApp |
| `.hit--ig-icon` | ícone do Instagram no rodapé | Instagram |
| `.hit--wa-icon` | ícone do WhatsApp no rodapé | WhatsApp |
| `.hit--loc` | "Surubim - PE" | Google Maps |

**Trocar o flyer:** substitua `assets/img/flyer.jpg` por outra imagem e atualize os
atributos `width` e `height` da tag `<img>` no `index.html`, o texto do `alt` e as
porcentagens das áreas. Se a nova imagem não for vertical 9:16, revise também o bloco
`@media (max-aspect-ratio: 9/16)` do CSS.

## Como funciona o preenchimento em telas altas

Em celulares mais compridos que o flyer, o espaço que sobra em cima e embaixo é
preenchido com as bordas do próprio flyer, espelhadas, desfocadas, escurecidas e com
degradê (pseudo-elementos `::before` e `::after` do `.page`), sem barras pretas chapadas.
O site também respeita a área segura do iPhone (`safe-area-inset`).
