<script lang="ts">
import { obterReceitas } from '@/http';
import type IReceita from '@/interfaces/IReceita';
import BotaoPrincipal from './BotaoPrincipal.vue';
import CardReceita from './CardReceita.vue';
import type { PropType } from 'vue';
type IIngrediente = String[]

export default {
    props: {
        ingredientes: { type: Array as PropType<IIngrediente>, required: true }
    },
    data() {
        return {
            receitas: [] as IReceita[]
        }
    },
    async created() {
        const receitasBuscadas = await obterReceitas();
        this.receitas = receitasBuscadas.filter(receita => 
            this.ingredientes.every(ingrediente => 
                receita.ingredientes.includes(ingrediente)
            )
        );
    },
    components: {
        BotaoPrincipal,
        CardReceita
    },
    emits: ['MostrarIngredientes']
}
</script>

<template>
    <div class="section">
        <h1 class="cabecalho titulo-ingredientes">Receitas</h1>
        <div v-if="receitas.length" class="section">
            <ul class="receitas mb">
                <li v-for="(receita, index) in receitas" :key="index">
                    <CardReceita :receita="receita" />
                </li>
            </ul>
            <BotaoPrincipal :titulo="'Realizar nova busca'" @click="$emit('MostrarIngredientes')"/>
        </div>
        <div v-else class="section">
            <p class="paragrafo-lg mb">
                Nossos chef's não encontraram nenhuma receita envolvendo os ingredientes :(
            </p>
            <BotaoPrincipal :titulo="'Voltar'" @click="$emit('MostrarIngredientes')"/>
        </div>
           
    </div>
</template>

<style scoped>
.section {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.titulo-ingredientes {
    color: var(--verde-medio, #3D6D4A);
    display: block;
    margin-bottom: 1.5rem;
}
.receitas {
    margin-bottom: 1rem;
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
}
.mb{
    margin-bottom: 20px;
}
</style>
