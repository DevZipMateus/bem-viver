# Seção de Produtos — Design Spec
**Data:** 2026-05-07
**Arquivo alvo:** `index.html` (seção `#produtos`)

---

## Contexto

O site da Bem Viver Distribuição (distribuidora oficial Royal Prestige) tem uma seção `#produtos` com:
- Banner da marca Royal Prestige com CTA WhatsApp
- Grid de 6 feature cards (benefícios: aço cirúrgico, nutrientes, garantia 50 anos, etc.)

A tarefa é adicionar uma sub-seção abaixo desses cards mostrando as 5 categorias do catálogo, com exemplos de produtos, botões de WhatsApp por categoria e download do catálogo PDF.

---

## Decisões de Design

### Estrutura geral
- **Manter** o conteúdo existente da seção (banner + 6 feature cards) sem alterações.
- **Adicionar** após os feature cards:
  1. Sub-header "Conheça nossas categorias"
  2. 5 blocos alternados (um por categoria)
  3. Faixa de download do catálogo

### Layout dos blocos (Opção B — Blocos Alternados)
Cada categoria ocupa um bloco horizontal com:
- **42% esquerda/direita:** imagem da categoria (cover, sem distorção)
- **58% restante:** conteúdo (tag de número, título, descrição, chips de produtos, botão WhatsApp)
- Direção da imagem alterna: esquerda → direita → esquerda → direita → esquerda

### Cores de fundo (alternância)
| # | Categoria | Fundo | Texto | Chips |
|---|-----------|-------|-------|-------|
| 1 | Panelas e Conjuntos | `--navy` (#1B2B5E) | branco | transparente/borda branca |
| 2 | Eletrodomésticos | `--cream2` (#F2EBD9) | navy | navy bg / gold-pale bg |
| 3 | Facas e muito mais | `white` | navy | navy bg / gold-pale bg |
| 4 | Café, chá e chocolate | `--navy` (#1B2B5E) | branco | transparente/borda branca |
| 5 | Acessórios de Cozinha | `--cream2` (#F2EBD9) | navy | navy bg / gold-pale bg |

### Imagens
Arquivos já existentes no diretório:
- `panelas.png` → Panelas e Conjuntos
- `eletrodomesticos.png` → Eletrodomésticos
- `facas.png` → Facas e muito mais
- `cafe,cha,chocolate.png` → Café, chá e chocolate
- `acessorios.png` → Acessórios de Cozinha

### Produtos de exemplo por categoria (chips)
Extraídos do catálogo PDF:

**Panelas e Conjuntos:**
- Sistema Profissional 15 Peças, Familiar 10 Peças, Clássico 7 Peças, Wok, Panela de Pressão

**Eletrodomésticos:**
- Power Blender, MaXtractor, 3 Filtros Intercambiáveis

**Facas e muito mais:**
- Jogo 5 Peças Chef, Facas para Churrasco, Cepo Acácia, Tábua de Bambu

**Café, chá e chocolate:**
- ExperTea, Royal Espresso 10 Xícaras, Canecas Térmicas

**Acessórios de Cozinha:**
- Utensílios de Silicone, Espátula Deluxe, Linha Premium

### Botão WhatsApp por categoria
Cada bloco terá um botão "Quero saber mais" abrindo `wa.me/5537999974066` com mensagem pré-preenchida via `?text=`:

| Categoria | Mensagem pré-preenchida |
|-----------|------------------------|
| Panelas e Conjuntos | `Olá! Tenho interesse nos Sistemas de Cozinha Royal Prestige (Panelas e Conjuntos). Poderia me enviar mais informações?` |
| Eletrodomésticos | `Olá! Tenho interesse nos Eletrodomésticos Royal Prestige (Power Blender e MaXtractor). Poderia me enviar mais informações?` |
| Facas e muito mais | `Olá! Tenho interesse na linha de Facas Royal Prestige. Poderia me enviar mais informações?` |
| Café, chá e chocolate | `Olá! Tenho interesse nos produtos de Café, Chá e Chocolate da Royal Prestige. Poderia me enviar mais informações?` |
| Acessórios de Cozinha | `Olá! Tenho interesse nos Acessórios de Cozinha Royal Prestige. Poderia me enviar mais informações?` |

Estilo do botão:
- Fundo navy → botão outline branco com ícone WhatsApp SVG inline
- Fundo claro → botão sólido `--navy` com ícone WhatsApp

### Faixa de download
- Fundo: gradiente navy `#111D40 → #253580`
- Ícone de documento PDF
- Texto: "Catálogo completo de Produtos Royal Prestige" + "PDF · 39 páginas"
- Botão dourado com ícone de download → `href="catalogo-produtos.pdf" download`

---

## CSS
- Nova CSS adicionada dentro do `<style>` existente, com prefixo `.cat-` para os seletores novos
- Animações `reveal` e `reveal-left`/`reveal-right` aplicadas nos blocos (sistema já existe no site)
- Responsivo: abaixo de 768px os blocos empilham verticalmente (imagem topo, conteúdo baixo)

---

## Integração no HTML
- Todo o novo HTML vai dentro do `<div class="container">` existente da seção `#produtos`, após o fechamento da `.features-grid`
- Não altera nenhum elemento existente
