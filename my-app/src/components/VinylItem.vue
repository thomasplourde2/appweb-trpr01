<script setup lang="ts">
    import { ref } from 'vue';
    import { type Vinyl } from '../types'
    defineProps<{ vinyls: Vinyl[] }>()
    const name = ref<string>('')
    const bandName = ref<string>('')
    const releaseYear = ref<string>('')
    const price = ref<string>('')
    const emit = defineEmits<{
    (event: 'clickRemove', vinyl: Vinyl): void;
    (event: 'clickAdd', name: string, bandName:string, releaseYear:string, price:string): void;
}>()
</script>

<template>
    <div class="card" style="width: 18rem;">
        <div class="card-header">
            Ajouter un Vinyle :
        </div>
        <div class="mb-3">
            <label for="albumName" class="form-label">Nom</label>
            <input v-model="name" class="form-control" id="albumName" placeholder="Nom de l'album">
        </div>
        <div class="mb-3">
            <label for="bandName" class="form-label">Nom groupe</label>
            <input v-model="bandName" class="form-control" id="bandName" placeholder="Nom du groupe">
        </div>
        <div class="mb-3">
            <label for="releaseYear" class="form-label">Date</label>
            <input v-model="releaseYear" class="form-control" id="releaseYear" placeholder="Date de sortie">
        </div>
        <div class="mb-3">
            <label for="price" class="form-label">Prix</label>
            <input v-model="price" class="form-control" id="price" placeholder="Prix">
        </div>
        <button @click="emit('clickAdd', name, bandName, releaseYear, price)" :disabled="!name.trim()">Ajouter</button>
    </div>
</template>

<style scoped>
</style>
