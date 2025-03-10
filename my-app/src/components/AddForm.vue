<script setup lang="ts">
    import { ref } from 'vue';
    import { type Vinyl } from '../types'
    const props = defineProps<{ vinylToDuplicate?: Vinyl }>();
    const name = ref<string>(props.vinylToDuplicate?.name || '')
    const bandName = ref<string>(props.vinylToDuplicate?.bandName || '')
    const releaseYear = ref<string>(props.vinylToDuplicate?.releaseYear?.toString() || '')
    const price = ref<string>(props.vinylToDuplicate?.price || '')
    const emit = defineEmits<{
    (event: 'clickAdd', name: string, bandName:string, releaseYear:number, price:string): void;
}>()

    const isYearValid = () => {
        return !isNaN(parseInt(releaseYear.value))
    }
    const isPriceValid = () => {
        return !isNaN(parseInt(price.value))
    }
    const isFormValid = () => {
        if(isYearValid() && isPriceValid()){
            return true
        }
        return false
    }
    const submitNewVinyl = () => {
        if(isFormValid()){
            emit('clickAdd', name.value, bandName.value, parseInt(releaseYear.value), price.value);
        }
    }
</script>

<template>
    <div class="card text-black text-bg-secondary mb-3" style="width: 20rem;">
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
            <div v-if="!isYearValid()" class="text-danger">L'année n'est pas valide.</div>
        </div>
        <div class="mb-3">
            <label for="price" class="form-label">Prix</label>
            <input v-model="price" class="form-control" id="price" placeholder="Prix du vinyle">
            <div v-if="!isPriceValid()" class="text-danger">Le prix n'est pas valide.</div>
        </div>
        <div class="mb-3 text-center">
            <button type="button" class="btn btn-dark" @click="submitNewVinyl"  :disabled="!name.trim() || !bandName.trim() || !releaseYear.trim() || !price.trim() || !isFormValid()">Ajouter</button>
        </div>
        </div>
    </div>
</template>

<style scoped>
</style>
