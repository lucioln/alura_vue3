<script lang="ts">
export default {
    props: {
        titulo: { type: String, required: true }
    }
}
</script>

<template>
    <button class="botao paragrafo-lg">
        {{ titulo }}
    </button>
</template>

<style scoped>
.botao {
    padding: 0.5rem 1rem;
    width: 19.5rem;
    height: 3.5rem;
    border-radius: 2rem;
    gap: 10px;
    color: var(--creme);
    background-color: #F0633C;
    box-shadow: 4px 4px 15px 0px rgba(255, 115, 76, 0.25);
    cursor: pointer;
    transition: 0.2s;
    font-weight: 700;

    display: flex;
    justify-content: center;
    align-items: center;
}

.botao:hover {
    background-color: var(--once-hover, #D1451E);
}
</style>