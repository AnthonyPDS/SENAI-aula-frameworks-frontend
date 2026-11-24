# Aula 5 — Criando APIs para o Front-end

**Disciplina:** Frameworks Front-end  
**Professor:** Prof. Me. Deivison S. Takatu  
**Repositório do Exercício:** [aula-5-Frameworks-Front-end](https://github.com/AnthonyPDS/aula-5-Frameworks-Front-end.git)

---

## 📌 Sumário da Aula
1. API (Application Programming Interface) e Protocolo HTTP
2. EndPoints e Formato JSON
3. Servidor Backend e Web Services
4. Criando uma API REST com Express.js e CORS
5. Hospedagem e Deploy no Render
6. Implementação Prática: API RESTful CRUD de Notas (`server.js` e `data.json`)
7. Documentação e Testes de API com Postman

---

## 1. Métodos HTTP e Endpoints

Uma **API** permite a comunicação entre cliente (Front-end) e servidor (Back-end) através de **Endpoints** (URLs específicas que dão acesso a recursos ou funcionalidades).

| Método | Finalidade | Características |
| :--- | :--- | :--- |
| **GET** | Recuperar informações do servidor | Seguro (não altera dados) e idempotente (várias chamadas retornam o mesmo resultado). |
| **POST** | Criar novos recursos no servidor | Não idempotente (chamadas repetidas criam múltiplos recursos). |
| **PUT** | Substituir completamente um recurso existente | Idempotente; utilizado para atualização total. |
| **PATCH** | Atualizar parcialmente um recurso | Utilizado para atualização parcial de campos. |
| **DELETE** | Remover um recurso específico | Idempotente (apagar algo já removido não altera o estado). |

---

## 2. JSON (JavaScript Object Notation)

Formato leve de troca de dados, fácil para humanos lerem/escreverem e para máquinas interpretarem (`parse`) e gerarem (`stringify`). Baseia-se em:
- **Objetos:** Coleções de pares `"chave": valor` (`{}`).
- **Arrays:** Listas ordenadas de valores (`[]`).

---

## 3. Servidor Backend, Web Service e Express.js

- **Servidor Backend:** Processa requisições, executa regras de negócio, gerencia a persistência de dados e fornece respostas aos clientes.
- **Web Service:** Serviço acessível via web (HTTP/HTTPS) que padroniza a comunicação entre sistemas heterogêneos (diferentes linguagens e plataformas).
- **Express.js:** Framework minimalista, rápido e flexível para **Node.js** que simplifica a criação de servidores web, roteamento (`/users`, `/api/notes`) e uso de **middlewares** (autenticação, logs, conversão de JSON e **CORS**).
- **CORS (Cross-Origin Resource Sharing):** Mecanismo de segurança do navegador que controla o acesso a recursos entre domínios diferentes.

---

## 4. Construindo uma API REST CRUD com Express

Exemplo prático desenvolvido na aula para gerenciamento de notas utilizando persistência em arquivo JSON (`data.json`):

### Dependências necessárias
```bash
npm install express cors body-parser
```

### Rotas da Aplicação (`/api/notes`)
- `GET /api/notes` — Lista todas as notas armazenadas.
- `POST /api/notes` — Cria uma nova nota (`id` gerado com `Date.now().toString()`, `titulo` e `texto`).
- `GET /api/notes/:id` — Retorna uma nota específica pelo ID.
- `PUT /api/notes/:id` — Atualiza `titulo` e `texto` de uma nota existente pelo ID (retorna `404` se não encontrada).
- `DELETE /api/notes/:id` — Remove uma nota filtrando pelo ID.

### Estrutura Base do Servidor (`server.js`)
```javascript
const express = require('express');
const bodyParser = require('body-parser');
const fs = require('fs');

const app = express();
const PORT = process.env.PORT || 3000;
const FILE = 'data.json';

app.use(bodyParser.json());
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', '*');
  next();
});

function readNotes() {
  try {
    return JSON.parse(fs.readFileSync(FILE));
  } catch {
    return [];
  }
}

function saveNotes(notes) {
  fs.writeFileSync(FILE, JSON.stringify(notes, null, 2));
}
```

---

## 5. Deploy e Documentação

- **Render (`render.com`):** Plataforma em nuvem para hospedagem de Web Services (Node.js, Python, etc.) com deploy contínuo integrado ao GitHub e SSL gratuito.
- **Vercel (`vercel.com`):** Plataforma utilizada para o deploy do Front-end em React consumindo a URL pública da API no Render.
- **Postman:** Ferramenta colaborativa para criar, testar, automatizar e documentar requisições HTTP por meio de **Coleções (Collections)**, variáveis de ambiente e Mock Servers.

---

## 💡 Pontos de Reflexão Arquitetural
- **Persistência em arquivo (`data.json`) vs. Banco de Dados:** Arquivos JSON são úteis para prototipagem e estudo, mas em produção apresentam problemas de concorrência (condições de corrida em escritas simultâneas), falta de indexação e queda de desempenho com grande volume de registros (ex.: 10.000+ notas), além de sistemas de arquivos efêmeros em plataformas cloud gratuitas.
- **Modularização:** Manter todo o código em `server.js` dificulta a manutenção. Boas práticas recomendam separar rotas (`routes/`), controladores (`controllers/`), regras de negócio/serviços (`services/`) e camada de dados (`models/` ou `repositories/`).
