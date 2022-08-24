<script setup>
defineProps({
    id: Number,
    title: String,
    body: {
        type: String,
        default: "Sin descripcion"
    },
    cambiarFavorito: Function
})

const emit = defineEmits(['cambiarFavorito'])

</script>
<template>
    <div class="card">
        <div class="card-body">
            <h5 class="title-card"> {{id}} - {{title}}</h5>
            <p>{{body}}</p>
            <button class="btn btn-outline-primary" @click="cambiarFavorito(title)">Favorito</button>
        </div>
    </div>
</template>

<style>

</style>