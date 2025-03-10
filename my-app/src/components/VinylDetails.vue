<script setup lang="ts">
    import { type Vinyl } from '../types'
    defineProps<{ vinyl?: Vinyl }>();
    const emit = defineEmits<{
    (event: 'closeDetails'): void;
}>()
</script>

<template>
    <div class="card text-black text-bg-info mb-3" style="width: 20rem;">
        <div class="card-header">
            Details du Vinyle :
        </div>
        <div class="row g-3 align-items-center p-2">
        <div class="mb-3">
            <p>Id : {{ vinyl?.id }}</p>
        </div>
        <div class="mb-3">
            <p>Nom de l'album : {{ vinyl?.name }}</p>
        </div>
        <div class="mb-3">
            <p>Nom du groupe : {{ vinyl?.bandName }}</p>
        </div>
        <div class="mb-3">
            <p>Année de sortie : {{ vinyl?.releaseYear }}</p>
        </div>
        <div class="mb-3">
            <p>Prix : {{ vinyl?.price }}$</p>
        </div>
        <div class="mb-3">
            <p>Quantité : {{ vinyl?.quantity }}</p>
        </div>
        <div class="mb-3 text-center">
            <button type="button" class="btn btn-dark" @click="emit('closeDetails')">Fermer</button>
        </div>
        </div>
    </div>
</template>

<style scoped>
</style>
