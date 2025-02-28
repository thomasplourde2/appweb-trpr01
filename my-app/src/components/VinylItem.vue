<script setup lang="ts">
    import { ref } from 'vue';
    //import { type Vinyl } from '../types'
    //defineProps<{ vinyls: Vinyl[] }>()
    const name = ref<string>('')
</script>

<template>
    <div>
        <p>Ajouter un Vinyle :</p>
        <input v-model="name" placeholder="Nom de l'album"/>
        <button>Ajouter</button>
    </div>
</template>

<style scoped>
</style>
