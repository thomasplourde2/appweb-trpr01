<script setup lang="ts">
    import { ref } from 'vue'
    import VinylItem from './VinylItem.vue'
    import { type Vinyl } from '../types'
    const showVinyl = ref(false)

    const showFormAddVinyl = () => {
        if(showVinyl.value)
          showVinyl.value = false
        else
          showVinyl.value = true
    }
    const vinyls = ref<Vinyl[]>([
])
const actionClickAdd = (vinylName:string, bandName:string, releaseYear:string, price:string) => {
    const newVinyl: Vinyl = {
        id: vinyls.value.length + 1,
        name: vinylName,
        bandName: bandName,
        releaseYear: releaseYear,
        price: price,
        quantity: + 1
    }
    vinyls.value.push(newVinyl);
}
</script>

<template>
  <div class=" p-3 bg-danger text-center"></div>
  <div class="d-flex justify-content gap-3 p-3 bg-dark-subtle">
    <button type="button" class="btn btn-outline-primary" @click="showFormAddVinyl">Ajouter un vinyle</button>
  </div>
  
  <VinylItem v-if="showVinyl" :vinyls="vinyls" @clickAdd="actionClickAdd"/>
</template>

<style scoped>
</style>
