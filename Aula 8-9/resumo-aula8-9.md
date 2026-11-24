# Aulas 8 e 9 — Projeto React (Parte 1 e Parte 2)

**Disciplina:** Frameworks Front-end  
**Professor:** Prof. Me. Deivison S. Takatu

---

## 📌 Visão Geral
Este resumo consolida os conteúdos das **Aulas 08 e 09**, cobrindo desde a revisão de JavaScript moderno e manipulação do DOM até a construção completa de aplicações **React** com componentes, props, estado (`useState`), formulários controlados, efeitos colaterais (`useEffect`), consumo de APIs REST e roteamento com **React Router**.

---

# Parte 1 — Revisão JavaScript e Fundamentos do React (Aula 08)

## 1. Revisão de JavaScript Essencial para React

- **Declaração de Variáveis e Escopo:**
  - `var`: escopo de função (evitar em código moderno).
  - `let`: escopo de bloco (`{}`), permite reatribuição.
  - `const`: escopo de bloco (`{}`), referência constante (padrão recomendado).
- **Tipos de Dados:** `String`, `Number`, `Boolean`, `Undefined`, `Null`, `Object`, `Array`, `Symbol` e `BigInt`. O operador `typeof` inspeciona o tipo do valor.
- **Operadores Importantes:**
  - Comparação estrita (`===` e `!==`): compara valor **e** tipo sem conversão implícita.
  - Operador ternário (`condicao ? valorSeVerdadeiro : valorSeFalso`): muito utilizado dentro do JSX.
  - Lógicos (`&&`, `||`, `!`) e Template Strings (`` `Olá, ${nome}!` ``).
- **Funções e Arrow Functions:**
  ```javascript
  function somar(a, b) { return a + b; }
  const multiplicar = (a, b) => a * b;
  ```
- **Arrays e Imutabilidade:** Métodos fundamentais no React como `.forEach()`, `.filter()` (filtra elementos que atendem a uma condição) e `.map()` (transforma cada item de um array em um novo elemento).
- **DOM (Document Object Model):** Representação em árvore do documento HTML no navegador (`querySelector`, `addEventListener`, `textContent`, `classList`).

---

## 2. JSX (JavaScript XML)

Extensão de sintaxe que permite escrever marcação semelhante a HTML diretamente dentro do JavaScript para descrever interfaces React.

- **Expressões JavaScript no JSX:** Utiliza-se chaves `{}` para interpolar variáveis, cálculos ou chamadas de função.
- **Principais Diferenças entre JSX e HTML:**
  - Usa `className` em vez de `class`.
  - Usa `htmlFor` em vez de `for`.
  - Todas as tags devem ser fechadas (ex.: `<img />`, `<input />`).
  - Todo componente deve retornar um **único elemento raiz** (ou um Fragment `<>...</>`).

```jsx
function Saudacao() {
  const nome = "João";
  return <h1 className="titulo">Olá, {nome}!</h1>;
}
```

---

## 3. Componentes e Props

### Componentes
São unidades independentes e reutilizáveis da interface. Em React moderno, são funções JavaScript iniciadas com **letra maiúscula** que retornam JSX:
- Organizam a aplicação em uma **árvore hierárquica** (ex.: `App` → `Cabecalho`, `BarraDePesquisa`, `ListaDeConceitos` → `CardConceito`, `Rodape`).

### Props (Propriedades)
Permitem passar dados de um **componente pai para um componente filho** (fluxo de dados unidirecional), tornando os componentes dinâmicos e reutilizáveis:

```jsx
function CardConceito({ titulo, descricao }) {
  return (
    <article>
      <h2>{titulo}</h2>
      <p>{descricao}</p>
    </article>
  );
}

// Utilização no componente Pai:
<CardConceito titulo="JSX" descricao="Sintaxe para descrever interfaces." />
<CardConceito titulo="Props" descricao="Entradas recebidas por componentes." />
```

---

## 4. Virtual DOM e Reconciliação

- **Virtual DOM:** Representação da interface mantida em memória pelo React.
- **Ciclo de Atualização:**
  1. **Mudança:** Ocorre uma alteração de estado ou dados.
  2. **Renderização:** O React reexecuta os componentes relevantes para gerar uma nova árvore virtual.
  3. **Reconciliação:** O React compara a nova descrição com a anterior (*diffing*).
  4. **Atualização:** Apenas as diferenças reais são aplicadas ao DOM do navegador.

---

## 5. Listas, Keys e Renderização Condicional

### Renderização de Listas e `key`
Utiliza-se `array.map()` para transformar coleções de dados em elementos JSX. Cada item da lista precisa de uma propriedade **`key` única e estável** (como o `id` do registro) para que o React identifique adições, remoções ou reordenações durante a reconciliação:

```jsx
{alunos.map((aluno) => (
  <li key={aluno.id}>{aluno.nome}</li>
))}
```

### Renderização Condicional
Permite exibir, ocultar ou alternar partes da interface conforme o estado ou props:
- **`if / return` antecipado:** Ideal quando a estrutura retornada muda completamente (ex.: lista vazia ou usuário não autenticado).
- **Operador Ternário (`? :`):** Ideal para alternar mensagens inline, como estados de carregamento (`carregando ? <p>Buscando...</p> : <p>Concluído!</p>`).

---

# Parte 2 — Estado, Hooks, Formulários, APIs e Rotas (Aula 09)

## 6. State e o Hook `useState`

Variáveis locais comuns não atualizam a tela quando mudam e são recriadas a cada renderização. Para guardar dados dinâmicos entre renderizações e atualizar a interface automaticamente, utilizamos o **State** através do Hook `useState`:

```jsx
import { useState } from "react";

function Contador() {
  const [contador, setContador] = useState(0);

  return (
    <section>
      <p>Valor: {contador}</p>
      <button onClick={() => setContador(contador + 1)}>
        Incrementar
      </button>
    </section>
  );
}
```
- **Regras dos Hooks:** Começam com o prefixo `use` e devem ser chamados sempre no nível superior (início) do componente funcional.

---

## 7. Formulários e Campos Controlados

Em React, formulários utilizam **Campos Controlados (Controlled Components)**, onde o valor do `<input>` é governado pelo estado do React:
- `value={estado}`: define o valor exibido no campo.
- `onChange={(e) => setEstado(e.target.value)}`: atualiza o estado a cada tecla digitada.
- `onSubmit` + `e.preventDefault()`: intercepta o envio do formulário e impede o recarregamento padrão da página pelo navegador.

```jsx
function FormularioCadastro() {
  const [nome, setNome] = useState("");

  function enviar(e) {
    e.preventDefault();
    alert(`Enviado com sucesso: ${nome}`);
  }

  return (
    <form onSubmit={enviar}>
      <input
        value={nome}
        onChange={(e) => setNome(e.target.value)}
        placeholder="Digite seu nome"
      />
      <button type="submit">Enviar</button>
    </form>
  );
}
```

---

## 8. Sincronização e Efeitos com `useEffect`

O Hook `useEffect` executa efeitos colaterais fora da pura renderização visual, sincronizando o componente com sistemas externos (APIs, título da aba do navegador, temporizadores, listeners de eventos globais).

```jsx
useEffect(() => {
  document.title = titulo;
}, [titulo]); // Executa quando 'titulo' muda
```

- **Array de Dependências:**
  - `[]` (vazio): executa apenas uma vez na montagem do componente.
  - `[dep1, dep2]`: reexecuta sempre que algum dos valores listados mudar.
- **Função de Limpeza (Cleanup):** Retornada dentro do `useEffect` para remover *event listeners*, cancelar *timers* ou abortar conexões quando o componente é desmontado ou antes de reexecutar o efeito.

---

## 9. Consumo de APIs com `fetch`

Combina `useEffect` (para disparar a busca na montagem) com `useState` (para armazenar os dados, estado de carregamento e tratamento de erros):

```jsx
useEffect(() => {
  async function carregar() {
    try {
      const resposta = await fetch("https://jsonplaceholder.typicode.com/posts");
      if (!resposta.ok) throw new Error("Erro na consulta HTTP");
      const dados = await resposta.json();
      setPublicacoes(dados);
    } catch (erro) {
      console.error(erro);
    }
  }
  carregar();
}, []);
```

### Enviando Dados com `POST`
```javascript
await fetch("/api/publicacoes", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ title: "Aprendendo React" })
});
```

---

## 10. Navegação e Páginas com React Router

O **React Router (`react-router-dom`)** permite criar aplicações de múltiplas telas (SPAs) associando URLs a componentes sem recarregar o documento no navegador:

- `<BrowserRouter>`: Envolve toda a aplicação para habilitar o controle de histórico de navegação.
- `<Routes>` e `<Route path="..." element={<Componente />} />`: Agrupam e definem qual componente será renderizado em cada rota.
- `<Link to="/sobre">`: Navega entre rotas internamente sem recarregar a página.
- `useParams()`: Hook que captura parâmetros dinâmicos da URL (ex.: rota `/conceitos/:id` → `const { id } = useParams()`).

```jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Início</Link> | <Link to="/sobre">Sobre</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Inicio />} />
        <Route path="/sobre" element={<Sobre />} />
        <Route path="/conceitos/:id" element={<DetalheConceito />} />
      </Routes>
    </BrowserRouter>
  );
}
```

### 🔗 Links Complementares das Aulas 08 e 09
- [Repositório de Conceitos React](https://github.com/deivisontakatu/aula-react)
- [Repositório do Projeto Exemplo React](https://github.com/deivisontakatu/projeto-react)
- [Aplicação Exemplo Publicada (Vercel)](https://projeto-react-five-swart.vercel.app/)
