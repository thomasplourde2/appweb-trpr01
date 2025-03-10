<script setup lang="ts">
    import { ref, watch, defineProps, defineEmits } from 'vue';
    import { type Vinyl } from '../types'
    const props = defineProps<{ vinyl: Vinyl }>()
    const name = ref<string>('')
    const bandName = ref<string>('')
    const releaseYear = ref<string>('')
    const price = ref<string>('')
    const quantity = ref<string>('')
    const emit = defineEmits<{
    (event: 'clickModify', id:number, vinylName:string, bandName:string, releaseYear:number, price:string, quantity:number): void;
}>()
watch(() => props.vinyl, (newVinyl) => {
    name.value = newVinyl.name;
    bandName.value = newVinyl.bandName;
    releaseYear.value = newVinyl.releaseYear.toString();
    price.value = newVinyl.price;
    quantity.value = newVinyl.quantity.toString();
}, { immediate: true });
    const isYearValid = () => {
        return !isNaN(parseInt(releaseYear.value))
    }
    const isPriceValid = () => {
        return !isNaN(parseInt(price.value))
    }
    const isQuantityValid = () => {
        return !isNaN(parseInt(quantity.value))
    }
    const isFormValid = () => {
        if(isYearValid() && isPriceValid() && isQuantityValid()){
            return true
        }
        return false
    }
    const submitModifiedVinyl = () => {
        if(isFormValid()){
            emit('clickModify', props.vinyl.id, name.value, bandName.value, parseInt(releaseYear.value), price.value, parseInt(quantity.value));
        }
    }
</script>

<template>
    <div class="card text-black text-bg-success mb-3" style="width: 20rem;">
        <div class="card-header">
            Modifier un Vinyle :
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
        <div class="mb-3">
            <label for="quantity" class="form-label">Quantité</label>
            <input v-model="quantity" class="form-control" id="quantity" placeholder="Quantité du vinyles">
            <div v-if="!isQuantityValid()" class="text-danger">La quantité n'est pas valide.</div>
        </div>
        <div class="mb-3 text-center">
            <button type="button" class="btn btn-dark" @click="submitModifiedVinyl"  :disabled="!name.trim() || !bandName.trim() || !releaseYear.trim() || !price.trim() || !quantity.trim() || !isFormValid()">Modifier</button>
        </div>
        </div>
    </div>
</template>

<style scoped>
</style>
