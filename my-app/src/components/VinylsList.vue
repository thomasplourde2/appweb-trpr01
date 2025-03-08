<script setup lang="ts">
    import { type Vinyl } from '../types'
    defineProps<{ vinyls: Vinyl[] }>()
    const emit = defineEmits<{
        (event: 'clickRemove', vinyl: Vinyl): void;
    }>()
</script>

<template>
    <table class="table table-dark table-striped" style="width: 60rem; height: 10rem;">
    <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Nom de l'album</th>
      <th scope="col">Nom du groupe</th>
      <th scope="col">Année de sortie</th>
      <th scope="col">Prix</th>
      <th scope="col">Quantité</th>
      <th scope="col">Options</th>
    </tr>
    </thead>
        <tbody v-if="vinyls.length > 0">
            <tr v-for="vinyl in vinyls" :key="vinyl.id">
                <th scope="row">{{ vinyl.id }}</th>
                <td>
                    {{ vinyl.name }}
                </td>
                <td>
                    {{ vinyl.bandName }}
                </td>
                <td>
                    {{ vinyl.releaseYear }}
                </td>
                <td>
                    {{ vinyl.price }}$
                </td>
                <td>
                    {{ vinyl.quantity }}
                </td>
                <td>
                    <div class="btn-group">
                        <button type="button" class="btn btn-danger btn-sm" @click="emit('clickRemove', vinyl)">
                            <i class="bi bi-trash"></i>
                        </button>
                        <button type="button" class="btn btn-success btn-sm">
                            <i class="bi bi-pencil"></i>
                        </button>
                        <button type="button" class="btn btn-primary btn-sm">
                            <i class="bi bi-copy"></i>
                        </button>
                        <button type="button" class="btn btn-info btn-sm">
                            <i class="bi bi-three-dots"></i>
                        </button>
                    </div>
                </td>
            </tr>
        </tbody>
        <p v-else>
            La liste est vide.
        </p>
    </table>
</template>

<style scoped>
</style>
