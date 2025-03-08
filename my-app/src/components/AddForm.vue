<script setup lang="ts">
    import { ref } from 'vue';
    const name = ref<string>('')
    const bandName = ref<string>('')
    const releaseYear = ref<string>('')
    const price = ref<string>('')
    const emit = defineEmits<{
    (event: 'clickAdd', name: string, bandName:string, releaseYear:number, price:string): void;
}>()
</script>

<template>
    <div class="card text-black text-bg-secondary mb-3" style="width: 20rem; height: 32rem;">
        <div class="card-header">
            Ajouter un Vinyle :
        </div>
        <div class="row g-3 align-items-center p-2">
        <div class="mb-3">
            <label for="albumName" class="form-label">Nom</label>
            <input v-model="name" class="form-control" id="albumName" placeholder="Nom de l'album">
        </div>
        <div class="mb-3">
            <label for="bandName" class="form-label">Nom groupe</label>
            <input v-model="bandName" class="form-control" id="bandName" placeholder="Nom du groupe">
        </div>
        <div class="mb-3">
            <label for="releaseYear" class="form-label">Année</label>
            <input v-model="releaseYear" class="form-control" id="releaseYear" placeholder="Année de sortie">
        </div>
        <div class="mb-3">
            <label for="price" class="form-label">Prix</label>
            <input v-model="price" class="form-control" id="price" placeholder="Prix du vinyle">
        </div>
        <div class="mb-3 text-center">
            <button type="button" class="btn" @click="emit('clickAdd', name, bandName, parseInt(releaseYear), price)"  :disabled="!name.trim() || !bandName.trim() || !releaseYear.trim() || !price.trim()">Ajouter</button>
        </div>
        </div>
    </div>
</template>

<style scoped>
</style>
