# Aula 7 — Frameworks CSS e Tailwind CSS

**Disciplina:** Frameworks Front-end  
**Professor:** Prof. Me. Deivison S. Takatu

---

## 📌 Sumário da Aula
1. Revisão de CSS (Cascading Style Sheets), Seletores e Propriedades
2. Formas de Aplicação do CSS (In-line, Interno e Externo)
3. Box Model (Modelo de Caixas)
4. Layout com Flexbox e Responsividade
5. O que é um Framework CSS?
6. Tailwind CSS e a Abordagem *Utility-First*
7. Instalação e Utilização do Tailwind CSS (Play CDN, CLI e IntelliSense)

---

## 1. Fundamentos de CSS

O **CSS** controla a apresentação visual das páginas HTML (cores, tipografia, dimensões, posicionamento e responsividade) usando a estrutura `seletor { propriedade: valor; }`.

### Formas de Aplicação
- **In-line (`style="..."`):** Aplicado diretamente na tag HTML. Indicado apenas para ajustes pontuais ou testes rápidos.
- **Interno (`<style>`):** Definido no `<head>` do documento HTML. Útil para estilos exclusivos de uma única página.
- **Externo (`<link rel="stylesheet" href="style.css">`):** Arquivo `.css` separado. **Forma mais recomendada**, pois centraliza a manutenção e permite reutilização em múltiplas páginas.

### Seletores de Classe e ID
- **Classes (`.nome-classe`):** Reutilizáveis em múltiplos elementos para manter consistência visual.
- **IDs (`#nome-id`):** Identificadores únicos na página, usados para elementos específicos, âncoras de navegação ou manipulação direta via JavaScript.

---

## 2. Box Model (Modelo de Caixas)

Todo elemento HTML é representado como uma caixa retangular composta por quatro camadas (de dentro para fora):

1. **Content (Conteúdo):** Área onde textos e imagens são exibidos (`width`, `height`).
2. **Padding (Preenchimento interno):** Espaço transparente entre o conteúdo e a borda.
3. **Border (Borda):** Linha que envolve o padding e o conteúdo (`border: 2px solid black`).
4. **Margin (Margem externa):** Espaço fora da borda que separa o elemento dos demais elementos vizinhos.

---

## 3. Flexbox e Layouts Responsivos

O **Flexbox (`display: flex`)** é um modelo de layout unidimensional para organizar, alinhar e distribuir espaço entre itens em uma linha ou coluna:

| Propriedade | Função | Valores Comuns |
| :--- | :--- | :--- |
| `flex-direction` | Define a direção do eixo principal | `row`, `column`, `row-reverse`, `column-reverse` |
| `justify-content` | Alinha os itens ao longo do eixo principal | `flex-start`, `center`, `flex-end`, `space-between`, `space-around`, `space-evenly` |
| `align-items` | Alinha os itens ao longo do eixo transversal | `flex-start`, `center`, `flex-end`, `stretch`, `baseline` |
| `flex-wrap` | Controla a quebra de linha dos itens | `nowrap`, `wrap`, `wrap-reverse` |
| `gap` | Define o espaçamento uniforme entre itens | `10px`, `1rem`, etc. |

### Responsividade
Adapta o layout para diferentes tamanhos de tela (celular, tablet e desktop), iniciando pela meta tag de viewport no HTML:
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

---

## 4. Frameworks CSS e Tailwind CSS

Um **Framework CSS** é um conjunto de recursos, padrões, classes e componentes baseados em **Layout** (Grid, Flexbox, responsividade), **Estilos** (cores, espaçamentos, tipografia) e **Componentes** (botões, cards, navbars). Exemplos: *Tailwind CSS, Bootstrap, Bulma, Foundation, Materialize*.

### Tailwind CSS (*Utility-First*)
Ao contrário de frameworks focados apenas em componentes prontos engessados, o **Tailwind CSS** adota o conceito **Utility-First**:
- Fornece pequenas classes utilitárias com responsabilidade única aplicadas diretamente no atributo `class` do HTML.
- **Ideia central:** *Uma utility = uma responsabilidade. Várias utilities combinadas = um componente.*

```html
<!-- Exemplo de botão estilizado com Tailwind CSS -->
<button class="bg-blue-600 text-white px-6 py-3 rounded-lg font-bold shadow">
  Enviar
</button>
```

| Classe Utilitária | Responsabilidade |
| :--- | :--- |
| `p-6` / `px-6 py-3` | Define o preenchimento interno (`padding`) |
| `text-xl` / `text-white` | Define tamanho e cor do texto |
| `font-bold` | Define o peso da fonte em negrito |
| `bg-blue-600` / `bg-white` | Define a cor de fundo (`background-color`) |
| `rounded-lg` / `rounded-xl` | Define bordas arredondadas (`border-radius`) |
| `shadow` | Aplica sombra ao elemento (`box-shadow`) |

### Formas de Importação do Tailwind CSS (v4)
1. **Play CDN (ideal para testes e prototipagem rápida):**
   ```html
   <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
   ```
2. **Tailwind CLI / PostCSS (para projetos e integração com frameworks):**
   ```bash
   npm install tailwindcss @tailwindcss/cli
   ```
   E no arquivo CSS principal:
   ```css
   @import "tailwindcss";
   ```

> **Dica de Produtividade:** Utilizar a extensão **Tailwind CSS IntelliSense** no VS Code para autocompletar classes, visualizar o CSS gerado em tempo real e evitar erros de digitação.
