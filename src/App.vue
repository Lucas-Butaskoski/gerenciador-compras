<template>
  <div class="pagina">
    <!-- Cabeçalho -->
    <header class="cabecalho">
      <div class="cabecalho-inner">
        <div class="logo">
          <span class="logo-icone">🛒</span>
          <span class="logo-texto">Minha Cesta</span>
        </div>
        <!-- Contador automático -->
        <div class="contador">
          <span class="contador-numero">{{ produtos.length }}</span>
          <span class="contador-label">{{ produtos.length === 1 ? 'item' : 'itens' }}</span>
        </div>
      </div>
    </header>

    <main class="conteudo">
      <!-- Formulário de adição -->
      <section class="secao-adicionar">
        <h1 class="titulo-principal">Gerenciador de <br /><em>Compras</em></h1>

        <div class="campo-adicionar">
          <!-- v-model para two-way data binding -->
          <input
            v-model="novoItem"
            @keyup.enter="adicionarProduto"
            type="text"
            placeholder="Digite o nome do produto..."
            class="input-produto"
            maxlength="60"
          />
          <button @click="adicionarProduto" class="btn-adicionar">
            Adicionar
          </button>
        </div>

        <!-- Feedback de erro com v-if -->
        <p v-if="mostrarErro" class="msg-erro">
          ⚠️ Por favor, digite o nome do produto antes de adicionar.
        </p>
      </section>

      <!-- Lista de produtos com v-if / v-else -->
      <section class="secao-lista">
        <!-- v-if: lista com itens -->
        <div v-if="produtos.length > 0">
          <h2 class="titulo-lista">Minha Cesta de Compras</h2>
          <ul class="lista-produtos">
            <!-- v-for com :key -->
            <ItemProduto
              v-for="produto in produtos"
              :key="produto.id"
              :nome="produto.nome"
              @remover="removerProduto(produto.id)"
            />
          </ul>
        </div>

        <!-- v-else: lista vazia -->
        <div v-else class="cesta-vazia">
          <div class="icone-vazio">🧺</div>
          <p class="texto-vazio">Sua cesta está vazia! Adicione produtos para começar.</p>
        </div>
      </section>
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import ItemProduto from './components/ItemProduto.vue'

// Variáveis reativas com ref()
const novoItem = ref('')
const produtos = ref([])
const mostrarErro = ref(false)
let proximoId = ref(1)

// Adicionar produto à lista
function adicionarProduto() {
  // Validação: não permite itens vazios
  if (!novoItem.value.trim()) {
    mostrarErro.value = true
    setTimeout(() => { mostrarErro.value = false }, 2500)
    return
  }

  // Manipulação de array: adiciona o novo produto
  produtos.value.push({
    id: proximoId.value++,
    nome: novoItem.value.trim()
  })

  // Limpa o campo de input
  novoItem.value = ''
  mostrarErro.value = false
}

// Remover produto pelo id
function removerProduto(id) {
  produtos.value = produtos.value.filter(p => p.id !== id)
}
</script>

<style scoped>
.pagina {
  min-height: 100vh;
  background: var(--creme);
}

/* --- Cabeçalho --- */
.cabecalho {
  background: var(--verde);
  padding: 0 24px;
  position: sticky;
  top: 0;
  z-index: 10;
  box-shadow: 0 2px 16px rgba(45, 106, 79, 0.18);
}

.cabecalho-inner {
  max-width: 640px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 64px;
}

.logo {
  display: flex;
  align-items: center;
  gap: 10px;
}

.logo-icone {
  font-size: 1.5rem;
}

.logo-texto {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 1.2rem;
  color: #fff;
  letter-spacing: -0.02em;
}

.contador {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: rgba(255,255,255,0.15);
  border-radius: 10px;
  padding: 6px 14px;
  min-width: 56px;
}

.contador-numero {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 1.3rem;
  color: #fff;
  line-height: 1;
}

.contador-label {
  font-size: 0.68rem;
  color: var(--verde-palido);
  text-transform: uppercase;
  letter-spacing: 0.06em;
}

/* --- Conteúdo --- */
.conteudo {
  max-width: 640px;
  margin: 0 auto;
  padding: 40px 24px 60px;
}

/* --- Seção adicionar --- */
.secao-adicionar {
  margin-bottom: 40px;
}

.titulo-principal {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 2.6rem;
  line-height: 1.1;
  letter-spacing: -0.03em;
  color: var(--verde);
  margin-bottom: 28px;
}

.titulo-principal em {
  font-style: italic;
  color: var(--laranja);
}

.campo-adicionar {
  display: flex;
  gap: 10px;
}

.input-produto {
  flex: 1;
  padding: 13px 16px;
  border: 2px solid var(--borda);
  border-radius: 12px;
  font-family: 'DM Sans', sans-serif;
  font-size: 1rem;
  background: #fff;
  color: var(--texto);
  outline: none;
  transition: border-color 0.2s, box-shadow 0.2s;
}

.input-produto::placeholder {
  color: #b0b0b0;
  font-weight: 300;
}

.input-produto:focus {
  border-color: var(--verde-claro);
  box-shadow: 0 0 0 3px rgba(82, 183, 136, 0.15);
}

.btn-adicionar {
  padding: 13px 22px;
  background: var(--verde);
  color: #fff;
  border: none;
  border-radius: 12px;
  font-family: 'Syne', sans-serif;
  font-weight: 600;
  font-size: 0.95rem;
  cursor: pointer;
  transition: background 0.2s, transform 0.15s;
  white-space: nowrap;
}

.btn-adicionar:hover {
  background: #235e44;
  transform: translateY(-1px);
}

.btn-adicionar:active {
  transform: translateY(0);
}

.msg-erro {
  margin-top: 10px;
  font-size: 0.88rem;
  color: var(--laranja);
  animation: aparecer 0.2s ease;
}

@keyframes aparecer {
  from { opacity: 0; transform: translateY(-4px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* --- Seção lista --- */
.titulo-lista {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 1.2rem;
  color: var(--texto-suave);
  margin-bottom: 16px;
  text-transform: uppercase;
  letter-spacing: 0.04em;
}

.lista-produtos {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

/* --- Cesta vazia --- */
.cesta-vazia {
  text-align: center;
  padding: 60px 20px;
  background: #fff;
  border: 2px dashed var(--borda);
  border-radius: 20px;
}

.icone-vazio {
  font-size: 3.5rem;
  margin-bottom: 16px;
}

.texto-vazio {
  font-size: 1.05rem;
  color: var(--texto-suave);
  font-weight: 300;
  max-width: 300px;
  margin: 0 auto;
  line-height: 1.6;
}
</style>
