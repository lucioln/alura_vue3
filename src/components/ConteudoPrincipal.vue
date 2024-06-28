<script lang="ts">
import MostrarReceitas from './MostrarReceitas.vue';
import SelecionarIngredientes from './SelecionarIngredientes.vue';
import Tag from './Tag.vue';

type Pagina = 'SelecionarIngredientes' | 'MostrarReceitas';

export default {
    data() {
        return {
            ingredientes: [] as string[],
            conteudo: 'SelecionarIngredientes' as Pagina
        }
    },
    components: {
        SelecionarIngredientes,
        MostrarReceitas,
        Tag,
    },
    methods: {
        adicionarIngredientes(ingrediente: any) {
            this.ingredientes.push(ingrediente)
        },
        removerIngredientes(ingrediente: any) {
            this.ingredientes = this.ingredientes.filter(x => x !== ingrediente)
        },
        navegar(pagina: Pagina) {
            this.conteudo = pagina
        }
    }
}
</script>

<template>
    <main class="conteudo-principal">
        <section v-if="conteudo === 'SelecionarIngredientes'">
            <span class="subtitulo-lg sua-lista-texto">
                Sua lista:
            </span>
            <ul class="ingredientes-sua-lista" v-if="ingredientes.length">
                <li v-for="(ingrediente, index) in ingredientes" :key="index">
                    <Tag :texto="ingrediente" ativa />
                </li>
            </ul>
            <p class="paragrafo lista-vazia" v-else>
                <img src="../assets/icons/lista-vazia.svg" alt="Ícone de pesquisa">
                Sua lista está vazia, selecione ingredientes para iniciar.
            </p>
            <SelecionarIngredientes 
                @adicionar-ingrediente="adicionarIngredientes($event)"
                @remover-ingrediente="removerIngredientes($event)" 
                @buscar-receitas="navegar('MostrarReceitas')"
                :ingredientesSelecionados="ingredientes"
                />
        </section>
        <section v-else-if="conteudo === 'MostrarReceitas'">
            <MostrarReceitas 
            :ingredientes
            @-mostrar-ingredientes="navegar('SelecionarIngredientes')" />
        </section>
    </main>
</template>

<style scoped>
.conteudo-principal {
    padding: 6.5rem 7.5rem;
    border-radius: 3.75rem 3.75rem 0rem 0rem;
    background: var(--creme, #FFFAF3);
    color: var(--cinza, #444);

    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 5rem;
}

.sua-lista-texto {
    color: var(--coral, #F0633C);
    display: block;
    text-align: center;
    margin-bottom: 1.5rem;
}

.ingredientes-sua-lista {
    display: flex;
    justify-content: center;
    gap: 1rem 1.5rem;
    flex-wrap: wrap;
}


.lista-vazia {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    gap: 0.25rem;

    color: var(--coral, #F0633C);
    text-align: center;
}

@media only screen and (max-width: 1300px) {
    .conteudo-principal {
        padding: 5rem 3.75rem;
        gap: 3.5rem;
    }
}

@media only screen and (max-width: 767px) {
    .conteudo-principal {
        padding: 4rem 1.5rem;
        gap: 4rem;
    }
}
</style>
