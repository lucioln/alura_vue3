<script lang="ts">
import type IReceita from '@/interfaces/IReceita';
import type { PropType } from 'vue';
export default {
    props: {
        receita: { type: Object as PropType<IReceita>, required: true }
    },
}
</script>

<template>
    <article class="receita">
        <img :src="`/imagens/receitas/${receita.imagem}`" class="imagem__card">
        <h2 class="titulo__card">
            {{ receita.nome }}
        </h2>
    </article>
</template>

<style scoped>
.receita {
    width: 19.5rem;
    padding: 1rem;
    border-radius: 1rem;
    background: var(--branco, #FFF);
    box-shadow: 4px 4px 10px 0px rgba(68, 68, 68, 0.05);
    height: 100%;

    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
}

.imagem__card {
    width: 282px;
    height: 150px;
    border-radius: 18px 18px 0 0;
}

.titulo__card {
    display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
