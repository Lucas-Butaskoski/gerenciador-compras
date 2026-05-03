<template>
  <li class="item-produto">
    <span class="item-nome">{{ nome }}</span>
    <button class="btn-remover" @click="$emit('remover')" title="Remover item">
      ✕
    </button>
  </li>
</template>

<script setup>
defineProps({
  nome: {
    type: String,
    required: true
  }
})

defineEmits(['remover'])
</script>

<style scoped>
.item-produto {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 18px;
  background: #fff;
  border: 1.5px solid var(--borda);
  border-radius: 12px;
  transition: box-shadow 0.2s, transform 0.2s;
  animation: entrar 0.25s ease;
}

.item-produto:hover {
  box-shadow: var(--sombra);
  transform: translateX(4px);
}

@keyframes entrar {
  from {
    opacity: 0;
    transform: translateY(-8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.item-nome {
  font-family: 'DM Sans', sans-serif;
  font-size: 1rem;
  font-weight: 400;
  color: var(--texto);
}

.btn-remover {
  background: transparent;
  border: 1.5px solid #e0e0e0;
  color: var(--laranja);
  border-radius: 8px;
  width: 32px;
  height: 32px;
  font-size: 0.75rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.2s, border-color 0.2s, transform 0.15s;
  flex-shrink: 0;
}

.btn-remover:hover {
  background: #fff1ee;
  border-color: var(--laranja);
  transform: scale(1.1);
}
</style>
