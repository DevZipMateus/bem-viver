# Seção de Categorias de Produtos Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Adicionar, abaixo dos 6 feature cards existentes na seção `#produtos`, cinco blocos alternados (um por categoria do catálogo) com imagem, descrição, chips de produtos, botão WhatsApp com mensagem pré-preenchida, e uma faixa de download do PDF do catálogo.

**Architecture:** Modificação única em `index.html` — novo CSS adicionado ao `<style>` existente (antes de `</style>`, linha 1416) e novo HTML adicionado dentro do `.container` da seção `#produtos` (após o fechamento de `.features-grid`, linha 1723). Nenhum arquivo novo é criado. As animações `.reveal-left` / `.reveal-right` já existem no CSS e são reutilizadas.

**Tech Stack:** HTML5 puro, CSS3 com variáveis CSS já declaradas no `:root` do site, sem dependências externas.

---

## Arquivos

| Ação | Arquivo | Linhas relevantes |
|------|---------|-------------------|
| Modificar | `index.html` | CSS: antes da linha 1416 (`</style>`); HTML: após linha 1723 (fechamento `.features-grid`), antes da linha 1724 (`</div>` do container) |

---

## Task 1: Adicionar CSS dos blocos de categorias

**Files:**
- Modify: `index.html:1415` (inserir antes de `</style>`)

- [ ] **Step 1: Localizar o ponto de inserção do CSS**

Abrir `index.html`. Linha 1416 contém `  </style>`. O novo CSS vai ser inserido imediatamente antes dessa linha.

- [ ] **Step 2: Inserir o bloco CSS completo**

No `index.html`, inserir o texto abaixo imediatamente antes de `  </style>` (linha 1416):

```css
    /* ═══════════════════════════════════════
       CATEGORIAS — blocos alternados
    ═══════════════════════════════════════ */
    .cat-sep {
      padding: 60px 0 20px;
      text-align: center;
    }
    .cat-sep .section-label { justify-content: center; }
    .cat-sep h3 {
      font-family: var(--font-display);
      font-size: clamp(1.8rem, 3vw, 2.4rem);
      font-weight: 600;
      color: var(--navy);
      line-height: 1.2;
      margin-bottom: 10px;
    }
    .cat-sep h3 em { font-style: italic; color: var(--gold); }
    .cat-sep p {
      font-size: 0.92rem;
      color: var(--text-mid);
      max-width: 540px;
      margin: 0 auto;
      line-height: 1.7;
    }

    .cat-blocks {
      overflow: hidden;
      margin: 32px -24px 0;
    }

    .cat-block {
      display: flex;
      align-items: stretch;
      border-top: 1px solid rgba(201,164,74,0.12);
    }
    .cat-block.rev { flex-direction: row-reverse; }
    .cat-block.bg-navy  { background: var(--navy-dark); }
    .cat-block.bg-cream { background: var(--cream-mid); }
    .cat-block.bg-white { background: var(--white); }

    .cat-img-wrap {
      width: 42%;
      flex-shrink: 0;
      position: relative;
      overflow: hidden;
      min-height: 320px;
    }
    .cat-img-wrap img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
      transition: transform 0.6s ease;
    }
    .cat-block:hover .cat-img-wrap img { transform: scale(1.04); }
    .cat-img-overlay {
      position: absolute;
      inset: 0;
      background: linear-gradient(135deg, rgba(27,43,94,0.2) 0%, transparent 60%);
      pointer-events: none;
    }

    .cat-content {
      flex: 1;
      padding: 48px 52px;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

    .cat-tag {
      font-family: var(--font-body);
      font-size: 0.68rem;
      font-weight: 700;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      margin-bottom: 10px;
    }
    .cat-tag-light { color: var(--gold-light); }
    .cat-tag-gold  { color: var(--gold); }

    .cat-title {
      font-family: var(--font-display);
      font-size: clamp(1.6rem, 2.5vw, 2.1rem);
      font-weight: 600;
      line-height: 1.15;
      margin-bottom: 14px;
    }
    .cat-title-white { color: var(--white); }
    .cat-title-navy  { color: var(--navy); }

    .cat-desc {
      font-size: 0.88rem;
      line-height: 1.75;
      margin-bottom: 20px;
    }
    .cat-desc-light { color: rgba(255,255,255,0.75); }
    .cat-desc-mid   { color: var(--text-mid); }

    .cat-chips {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin-bottom: 28px;
    }
    .chip {
      padding: 4px 12px;
      border-radius: 5px;
      font-size: 0.68rem;
      font-weight: 600;
      letter-spacing: 0.03em;
      white-space: nowrap;
    }
    .chip-light { background: rgba(255,255,255,0.1);  border: 1px solid rgba(255,255,255,0.22); color: rgba(255,255,255,0.9); }
    .chip-navy  { background: var(--navy);             color: var(--gold-light); }
    .chip-pale  { background: var(--gold-pale);        border: 1px solid rgba(201,164,74,0.35); color: var(--navy); }

    .cat-wa-btn {
      display: inline-flex;
      align-items: center;
      gap: 9px;
      font-family: var(--font-body);
      font-size: 0.75rem;
      font-weight: 700;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      padding: 10px 20px;
      border-radius: 9px;
      border: none;
      cursor: pointer;
      text-decoration: none;
      transition: transform 0.2s, box-shadow 0.2s, background 0.2s, border-color 0.2s;
      align-self: flex-start;
    }
    .cat-wa-btn svg { width: 17px; height: 17px; flex-shrink: 0; }

    .cat-wa-outline {
      background: rgba(255,255,255,0.08);
      color: var(--white);
      border: 1px solid rgba(255,255,255,0.3);
    }
    .cat-wa-outline:hover {
      background: rgba(255,255,255,0.15);
      border-color: rgba(255,255,255,0.6);
      transform: translateY(-2px);
    }
    .cat-wa-solid {
      background: var(--navy);
      color: var(--white);
      box-shadow: 0 4px 16px rgba(27,43,94,0.2);
    }
    .cat-wa-solid:hover {
      background: var(--navy-light);
      transform: translateY(-2px);
      box-shadow: 0 8px 24px rgba(27,43,94,0.3);
    }

    .cat-dl-strip {
      background: linear-gradient(135deg, var(--navy-dark) 0%, var(--navy-light) 100%);
      padding: 28px 52px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 20px;
      flex-wrap: wrap;
    }
    .cat-dl-left {
      display: flex;
      align-items: center;
      gap: 16px;
    }
    .cat-dl-icon {
      width: 44px; height: 44px;
      border-radius: 10px;
      background: rgba(201,164,74,0.15);
      border: 1px solid rgba(201,164,74,0.3);
      display: flex; align-items: center; justify-content: center;
      flex-shrink: 0;
    }
    .cat-dl-icon svg { width: 22px; height: 22px; fill: var(--gold-light); }
    .cat-dl-text strong {
      display: block;
      color: var(--white);
      font-size: 0.9rem;
      margin-bottom: 2px;
    }
    .cat-dl-text span { color: rgba(255,255,255,0.5); font-size: 0.72rem; }
    .cat-dl-btn {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: var(--gold);
      color: var(--navy-dark);
      font-family: var(--font-body);
      font-size: 0.76rem;
      font-weight: 700;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      padding: 11px 22px;
      border-radius: 9px;
      text-decoration: none;
      transition: background 0.25s, transform 0.2s, box-shadow 0.25s;
      box-shadow: 0 4px 20px rgba(201,164,74,0.3);
      white-space: nowrap;
    }
    .cat-dl-btn svg { width: 16px; height: 16px; }
    .cat-dl-btn:hover {
      background: var(--gold-light);
      transform: translateY(-2px);
      box-shadow: 0 8px 28px rgba(201,164,74,0.45);
    }

    @media (max-width: 768px) {
      .cat-block,
      .cat-block.rev { flex-direction: column; }
      .cat-img-wrap  { width: 100%; min-height: 220px; }
      .cat-content   { padding: 32px 24px; }
      .cat-dl-strip  { padding: 24px; flex-direction: column; align-items: flex-start; }
    }
    @media (max-width: 480px) {
      .cat-content { padding: 24px 20px; }
    }
```

- [ ] **Step 3: Verificar que o CSS foi inserido corretamente**

```bash
grep -n "cat-blocks\|cat-block\|cat-wa-btn\|cat-dl-strip" index.html | head -10
```

Resultado esperado: pelo menos 10 linhas com os seletores acima.

---

## Task 2: Adicionar HTML da sub-seção de categorias

**Files:**
- Modify: `index.html:1723` (inserir após `</div>` que fecha `.features-grid`, antes do `</div>` que fecha `.container`)

A linha 1723 é `        </div>` (fecha `.features-grid`). A linha 1724 é `      </div>` (fecha `.container`). O novo HTML vai entre essas duas linhas.

- [ ] **Step 1: Inserir o HTML completo após o fechamento de `.features-grid`**

No `index.html`, encontrar o trecho exato:

```html
          </div>
        </div>
      </div>
    </section>

    <!-- ═══════════════════════════════════════
         MISSÃO, VISÃO E VALORES
```

E substituir por:

```html
          </div>
        </div>

        <!-- ═══════════════════════════════════════
             CATEGORIAS — blocos alternados
        ═══════════════════════════════════════ -->
        <div class="cat-sep reveal">
          <div class="section-label" aria-hidden="true">Catálogo completo</div>
          <h3>Conheça nossas <em>categorias</em></h3>
          <p>Da cozinha ao café da manhã, temos tudo para transformar sua experiência à mesa.</p>
        </div>

        <div class="cat-blocks">

          <!-- 1. PANELAS E CONJUNTOS — navy, img esquerda -->
          <div class="cat-block bg-navy reveal-left">
            <div class="cat-img-wrap">
              <img src="panelas.png" alt="Panelas e Conjuntos Royal Prestige — sistemas de cozinha em aço cirúrgico" width="600" height="400" loading="lazy">
              <div class="cat-img-overlay" aria-hidden="true"></div>
            </div>
            <div class="cat-content">
              <div class="cat-tag cat-tag-light" aria-hidden="true">Categoria 01</div>
              <h3 class="cat-title cat-title-white">Panelas e Conjuntos</h3>
              <p class="cat-desc cat-desc-light">Sistemas de cozinha em aço cirúrgico 316L fabricados na Itália. Cozinhe sem óleo com a tecnologia Redi-Temp™ e garantia limitada de até 50 anos, compatíveis com todos os tipos de fogão.</p>
              <div class="cat-chips" role="list" aria-label="Produtos desta categoria">
                <span class="chip chip-light" role="listitem">Profissional 15 Peças</span>
                <span class="chip chip-light" role="listitem">Familiar 10 Peças</span>
                <span class="chip chip-light" role="listitem">Clássico 7 Peças</span>
                <span class="chip chip-light" role="listitem">Wok</span>
                <span class="chip chip-light" role="listitem">Panela de Pressão</span>
              </div>
              <a
                href="https://wa.me/5537999974066?text=Ol%C3%A1%21%20Tenho%20interesse%20nos%20Sistemas%20de%20Cozinha%20Royal%20Prestige%20%28Panelas%20e%20Conjuntos%29.%20Poderia%20me%20enviar%20mais%20informa%C3%A7%C3%B5es%3F"
                target="_blank"
                rel="noopener noreferrer"
                class="cat-wa-btn cat-wa-outline"
                aria-label="Perguntar sobre Panelas e Conjuntos pelo WhatsApp"
              >
                <svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/></svg>
                Quero saber mais
              </a>
            </div>
          </div>

          <!-- 2. ELETRODOMÉSTICOS — cream, img direita -->
          <div class="cat-block rev bg-cream reveal-right">
            <div class="cat-img-wrap">
              <img src="eletrodomesticos.png" alt="Eletrodomésticos Royal Prestige — liquidificador e extrator de sucos" width="600" height="400" loading="lazy">
              <div class="cat-img-overlay" aria-hidden="true"></div>
            </div>
            <div class="cat-content">
              <div class="cat-tag cat-tag-gold" aria-hidden="true">Categoria 02</div>
              <h3 class="cat-title cat-title-navy">Eletrodomésticos</h3>
              <p class="cat-desc cat-desc-mid">Todo o poder que sua cozinha precisa. Liquidificador de alta potência com motor de 2cv e 6 lâminas de aço inoxidável, e extrator de sucos lento MaXtractor com 3 filtros intercambiáveis.</p>
              <div class="cat-chips" role="list" aria-label="Produtos desta categoria">
                <span class="chip chip-navy" role="listitem">Power Blender</span>
                <span class="chip chip-navy" role="listitem">MaXtractor</span>
                <span class="chip chip-pale" role="listitem">3 Filtros Intercambiáveis</span>
              </div>
              <a
                href="https://wa.me/5537999974066?text=Ol%C3%A1%21%20Tenho%20interesse%20nos%20Eletrodom%C3%A9sticos%20Royal%20Prestige%20%28Power%20Blender%20e%20MaXtractor%29.%20Poderia%20me%20enviar%20mais%20informa%C3%A7%C3%B5es%3F"
                target="_blank"
                rel="noopener noreferrer"
                class="cat-wa-btn cat-wa-solid"
                aria-label="Perguntar sobre Eletrodomésticos pelo WhatsApp"
              >
                <svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/></svg>
                Quero saber mais
              </a>
            </div>
          </div>

          <!-- 3. FACAS E MUITO MAIS — white, img esquerda -->
          <div class="cat-block bg-white reveal-left">
            <div class="cat-img-wrap">
              <img src="facas.png" alt="Facas Royal Prestige — jogos de facas e cepo de madeira acácia" width="600" height="400" loading="lazy">
              <div class="cat-img-overlay" aria-hidden="true"></div>
            </div>
            <div class="cat-content">
              <div class="cat-tag cat-tag-gold" aria-hidden="true">Categoria 03</div>
              <h3 class="cat-title cat-title-navy">Facas e muito mais</h3>
              <p class="cat-desc cat-desc-mid">Lâminas de aço inoxidável de alta qualidade, já afiadas de fábrica. Cepo de madeira acácia natural com afiador integrado para até 17 ferramentas e tábuas de bambu antibacterianas.</p>
              <div class="cat-chips" role="list" aria-label="Produtos desta categoria">
                <span class="chip chip-navy" role="listitem">Jogo 5 Peças Chef</span>
                <span class="chip chip-navy" role="listitem">Facas para Churrasco</span>
                <span class="chip chip-pale" role="listitem">Cepo Acácia</span>
                <span class="chip chip-pale" role="listitem">Tábua de Bambu</span>
              </div>
              <a
                href="https://wa.me/5537999974066?text=Ol%C3%A1%21%20Tenho%20interesse%20na%20linha%20de%20Facas%20Royal%20Prestige.%20Poderia%20me%20enviar%20mais%20informa%C3%A7%C3%B5es%3F"
                target="_blank"
                rel="noopener noreferrer"
                class="cat-wa-btn cat-wa-solid"
                aria-label="Perguntar sobre Facas e mais pelo WhatsApp"
              >
                <svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/></svg>
                Quero saber mais
              </a>
            </div>
          </div>

          <!-- 4. CAFÉ, CHÁ E CHOCOLATE — navy, img direita -->
          <div class="cat-block rev bg-navy reveal-right">
            <div class="cat-img-wrap">
              <img src="cafe,cha,chocolate.png" alt="Café, chá e chocolate Royal Prestige — chaleira, cafeteira e canecas térmicas" width="600" height="400" loading="lazy">
              <div class="cat-img-overlay" aria-hidden="true"></div>
            </div>
            <div class="cat-content">
              <div class="cat-tag cat-tag-light" aria-hidden="true">Categoria 04</div>
              <h3 class="cat-title cat-title-white">Café, chá e chocolate</h3>
              <p class="cat-desc cat-desc-light">Utensílios ideais para aproveitar os momentos mais especiais do dia. Da chaleira ExperTea em aço cirúrgico T-304 à cafeteira espresso e canecas térmicas que mantêm suas bebidas quentes por mais tempo.</p>
              <div class="cat-chips" role="list" aria-label="Produtos desta categoria">
                <span class="chip chip-light" role="listitem">ExperTea</span>
                <span class="chip chip-light" role="listitem">Royal Espresso 10 Xícaras</span>
                <span class="chip chip-light" role="listitem">Canecas Térmicas</span>
              </div>
              <a
                href="https://wa.me/5537999974066?text=Ol%C3%A1%21%20Tenho%20interesse%20nos%20produtos%20de%20Caf%C3%A9%2C%20Ch%C3%A1%20e%20Chocolate%20da%20Royal%20Prestige.%20Poderia%20me%20enviar%20mais%20informa%C3%A7%C3%B5es%3F"
                target="_blank"
                rel="noopener noreferrer"
                class="cat-wa-btn cat-wa-outline"
                aria-label="Perguntar sobre Café, Chá e Chocolate pelo WhatsApp"
              >
                <svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/></svg>
                Quero saber mais
              </a>
            </div>
          </div>

          <!-- 5. ACESSÓRIOS DE COZINHA — cream, img esquerda -->
          <div class="cat-block bg-cream reveal-left">
            <div class="cat-img-wrap">
              <img src="acessorios.png" alt="Acessórios de Cozinha Royal Prestige" width="600" height="400" loading="lazy">
              <div class="cat-img-overlay" aria-hidden="true"></div>
            </div>
            <div class="cat-content">
              <div class="cat-tag cat-tag-gold" aria-hidden="true">Categoria 05</div>
              <h3 class="cat-title cat-title-navy">Acessórios de Cozinha</h3>
              <p class="cat-desc cat-desc-mid">Complete sua cozinha com acessórios desenvolvidos para facilitar o preparo e a apresentação dos seus pratos. Qualidade e durabilidade em cada detalhe.</p>
              <div class="cat-chips" role="list" aria-label="Produtos desta categoria">
                <span class="chip chip-navy" role="listitem">Utensílios de Silicone</span>
                <span class="chip chip-navy" role="listitem">Espátula Deluxe</span>
                <span class="chip chip-pale" role="listitem">Linha Premium</span>
              </div>
              <a
                href="https://wa.me/5537999974066?text=Ol%C3%A1%21%20Tenho%20interesse%20nos%20Acess%C3%B3rios%20de%20Cozinha%20Royal%20Prestige.%20Poderia%20me%20enviar%20mais%20informa%C3%A7%C3%B5es%3F"
                target="_blank"
                rel="noopener noreferrer"
                class="cat-wa-btn cat-wa-solid"
                aria-label="Perguntar sobre Acessórios de Cozinha pelo WhatsApp"
              >
                <svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/></svg>
                Quero saber mais
              </a>
            </div>
          </div>

          <!-- FAIXA DE DOWNLOAD DO CATÁLOGO -->
          <div class="cat-dl-strip reveal">
            <div class="cat-dl-left">
              <div class="cat-dl-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8l-6-6zm-1 7V3.5L18.5 9H13zm-1 8l-4-4h3v-2h2v2h3l-4 4z"/></svg>
              </div>
              <div class="cat-dl-text">
                <strong>Catálogo completo de Produtos Royal Prestige</strong>
                <span>PDF · 39 páginas · todas as linhas e especificações técnicas</span>
              </div>
            </div>
            <a
              href="catalogo-produtos.pdf"
              download="Catalogo-Royal-Prestige.pdf"
              class="cat-dl-btn"
              aria-label="Baixar catálogo completo de produtos em PDF"
            >
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" aria-hidden="true"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="7,10 12,15 17,10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
              Baixar Catálogo PDF
            </a>
          </div>

        </div>
      </div>
    </section>

    <!-- ═══════════════════════════════════════
         MISSÃO, VISÃO E VALORES
```

- [ ] **Step 2: Verificar que a seção foi inserida e o HTML está balanceado**

```bash
grep -c "cat-block\|cat-wa-btn\|cat-dl-strip" index.html
```

Resultado esperado: número maior que 10.

```bash
python3 -c "
from html.parser import HTMLParser
class Check(HTMLParser):
    def __init__(self):
        super().__init__()
        self.stack = []
        self.errors = []
    def handle_starttag(self, tag, attrs):
        void = {'area','base','br','col','embed','hr','img','input','link','meta','param','source','track','wbr'}
        if tag not in void: self.stack.append(tag)
    def handle_endtag(self, tag):
        if self.stack and self.stack[-1] == tag: self.stack.pop()
        else: self.errors.append(f'Unexpected </{tag}>')
p = Check()
p.feed(open('index.html').read())
print('Errors:', p.errors[:5] if p.errors else 'none')
print('Unclosed:', p.stack[-5:] if p.stack else 'none')
"
```

Resultado esperado: `Errors: none` e `Unclosed: none` (ou apenas tags intencionalmente abertas como `html`, `body`).

---

## Task 3: Verificação visual no browser

**Files:** Nenhuma modificação — somente verificação.

- [ ] **Step 1: Abrir o site no browser**

```bash
xdg-open /home/ramal614/Documentos/desenv-claude/bem-viver/index.html 2>/dev/null || echo "abrir manualmente no browser"
```

- [ ] **Step 2: Verificar checklist visual**

Navegar até a seção `#produtos` e confirmar:

1. Sub-header "Conheça nossas categorias" visível com label dourado e título em itálico
2. Bloco 1 (Panelas) — fundo navy, imagem à esquerda, texto branco, botão outline branco
3. Bloco 2 (Eletrodomésticos) — fundo creme, imagem à direita, texto navy, botão navy sólido
4. Bloco 3 (Facas) — fundo branco, imagem à esquerda, texto navy, botão navy sólido
5. Bloco 4 (Café) — fundo navy, imagem à direita, texto branco, botão outline branco
6. Bloco 5 (Acessórios) — fundo creme, imagem à esquerda, texto navy, botão navy sólido
7. Faixa de download — fundo gradiente navy, botão dourado "Baixar Catálogo PDF"
8. Hover sobre cada imagem — zoom suave
9. Redimensionar janela abaixo de 768px — blocos empilham verticalmente

- [ ] **Step 3: Verificar links WhatsApp**

Clicar em um botão "Quero saber mais" — o WhatsApp deve abrir com a mensagem pré-preenchida correspondente à categoria. Confirmar que o número `5537999974066` aparece corretamente.

- [ ] **Step 4: Verificar download do catálogo**

Clicar em "Baixar Catálogo PDF" — o browser deve iniciar o download de `catalogo-produtos.pdf` com o nome `Catalogo-Royal-Prestige.pdf`.
