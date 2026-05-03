# 🛒 Gerenciador de Compras

**Aluno:** Lucas Butaskoski

Atividade Avaliativa N1 — Frameworks Modernos para Desenvolvimento de Sistemas  
6º Período — Sistemas de Informação — UNEMAT  
Prof. Me. Cides S. Bezerra

---

## Sobre o Projeto

Sistema de Gestão de Compras desenvolvido com **Vue.js 3 + Vite**, aplicando os conceitos de:

- `ref()` — variáveis reativas para controle de estado
- `v-model` — two-way data binding no campo de input
- `v-for` com `:key` — renderização dinâmica da lista de produtos
- `v-if` / `v-else` — exibição condicional (lista com itens vs. cesta vazia)
- Manipulação de arrays — métodos para adicionar e remover itens

## Funcionalidades

- ✅ Adicionar produto pelo botão ou tecla **Enter**
- ✅ Validação: não permite adicionar itens vazios
- ✅ Exibe **"Minha Cesta de Compras"** quando há itens
- ✅ Exibe mensagem de cesta vazia quando não há itens
- ✅ Remoção individual de cada produto
- ✅ Contador automático de itens no cabeçalho

## Estrutura do Projeto

```
src/
├── components/
│   └── ItemProduto.vue   # Componente de cada item da lista
├── App.vue               # Componente principal
├── main.js               # Ponto de entrada da aplicação
└── style.css             # Estilos globais
```

## Como Executar

```bash
# Instalar dependências
npm install

# Iniciar servidor de desenvolvimento
npm run dev
```

Acesse em: `http://localhost:5173`
