<script setup lang="ts">
    import { ref } from 'vue'
    import AddForm from './AddForm.vue'
    import { type Vinyl } from '../types'
    import VinylsList from './VinylsList.vue'
    import ModifyForm from './ModifyForm.vue'
    import VinylDetails from './VinylDetails.vue'
    const showVinylAddForm = ref(false)
    const showVinylModifyForm = ref(false)
    const showVinylDetails = ref(false)
    const selectedVinyl = ref<Vinyl>();
    const searchContent = ref('');

    const showFormAddVinyl = () => {
        const emptyVinyl: Vinyl = {
            id: 0,
            name: '',
            bandName: '',
            releaseYear: 0,
            price: '',
            quantity: 0
        }
        selectedVinyl.value = emptyVinyl
        if(showVinylAddForm.value)
        showVinylAddForm.value = false
        else
        showVinylAddForm.value = true
    }
    const vinyls = ref<Vinyl[]>([
      {id:1, name:"In Utero", bandName:"Nirvana", releaseYear:1993, price:"39,99", quantity:6},
      {id:2, name:"Sister", bandName:"Sonic Youth", releaseYear:1987, price:"34,99", quantity:2},
      {id:3, name:"Where You Been", bandName:"Dinosaur Jr.", releaseYear:1993, price:"59,99", quantity:3},
      {id:4, name:"Superfuzz Bigmuff", bandName:"Mudhoney", releaseYear:1988, price:"31,99", quantity:1},
      {id:5, name:"Ten", bandName:"Pearl Jam", releaseYear:1991, price:"36,99", quantity:5},
      {id:6, name:"Amnesiac", bandName:"Radiohead", releaseYear:2001, price:"47,99", quantity:2},
      {id:7, name:"Mellon Collie And The Infinite Sadness", bandName:"The Smashing Pumpkins", releaseYear:1995, price:"74,99", quantity:1},
      {id:8, name:"Sweet Oblivion", bandName:"Screaming Trees", releaseYear:1992, price:"27,99", quantity:2},
      {id:9, name:"Live Through This", bandName:"Hole", releaseYear:1993, price:"42,99", quantity:4},
      {id:10, name:"Loveless", bandName:"My Bloody Valentine", releaseYear:1991, price:"41,99", quantity:3}
])
const actionClickAdd = (vinylName:string, bandName:string, releaseYear:number, price:string) => {
    const newVinyl: Vinyl = {
        id: vinyls.value.length + 1,
        name: vinylName,
        bandName: bandName,
        releaseYear: releaseYear,
        price: price,
        quantity: + 1
    }
    vinyls.value.push(newVinyl);
    showVinylAddForm.value = false
}
const actionClickRemove = (vinyl:Vinyl) => {
    for (let i = 0; i < vinyls.value.length; i++) {
        if (vinyls.value[i].id === vinyl.id) {
          vinyls.value.splice(i, 1)
        }
    }
    for (let i = 0; i < vinyls.value.length; i++) {
      vinyls.value[i].id = i+1;
    }
}
const actionShowModifyForm = (vinyl:Vinyl) => {
  showVinylModifyForm.value = true
  selectedVinyl.value = vinyl
}
const actionClickModify = (id:number, vinylName:string, bandName:string, releaseYear:number, price:string, quantity:number) => {
  const newVinyl: Vinyl = {
        id: id,
        name: vinylName,
        bandName: bandName,
        releaseYear: releaseYear,
        price: price,
        quantity: quantity
    }
    vinyls.value[id-1] = newVinyl
    showVinylModifyForm.value = false
}
const actionClickDuplicate = (vinyl: Vinyl) => {
  selectedVinyl.value = vinyl
  showVinylAddForm.value = true
};
const actionClickDetails = (vinyl: Vinyl) => {
  selectedVinyl.value = vinyl
  showVinylDetails.value = true
};
const actionCloseDetails = () => {
  showVinylDetails.value = false
};
const filterVinyls = () => {
    return vinyls.value.filter(vinyl =>
    vinyl.name.toLowerCase().includes(searchContent.value.toLowerCase()))
};
const exportToCSV = () => {
  const headers = ["ID,Nom,Nom du Groupe,Année de sortie,Prix,Quantité"];
  const rows = vinyls.value.map(vinyl =>
    `${vinyl.id},"${vinyl.name}","${vinyl.bandName}",${vinyl.releaseYear},${vinyl.price},${vinyl.quantity}`
  );

  const csvContent = [headers, ...rows].join("\n");
  const blob = new Blob([csvContent], { type: "text/csv;charset=utf-8;" });
  const url = URL.createObjectURL(blob);
  
  const link = document.createElement("a");
  link.href = url;
  link.setAttribute("download", "vinyls.csv");
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
};
</script>

<template>
    <main class="bg-dark">
      <div class=" p-1 bg-danger"></div>
      <div class="d-flex justify-content gap-3 p-3 bg-black">
        <button type="button" class="btn btn-outline-secondary" @click="showFormAddVinyl">
          Ajouter un vinyle <i class="bi bi-plus-square"></i>
        </button>
        <div class="d-flex justify-content-center">
          <input v-model="searchContent" class="form-control" placeholder="Rechercher un vinyle..." />
        </div>
        <button type="button" class="btn btn-outline-secondary" @click="exportToCSV">
          Exporter en CSV <i class="bi bi-file-earmark-spreadsheet"></i>
        </button>
      </div>
      <div class=" p-1 bg-danger"></div>
      <h1 class="text-danger text-center">Liste des Vinyles</h1>
      <div class="d-flex justify-content-evenly">
        <AddForm class="m-3" v-if="showVinylAddForm" @clickAdd="actionClickAdd" :vinylToDuplicate="selectedVinyl"/>
        <VinylsList class="m-3" :vinyls="filterVinyls()" @clickRemove="actionClickRemove" @clickShowModify="actionShowModifyForm" @clickDuplicate="actionClickDuplicate" @clickDetails="actionClickDetails"/>
        <VinylDetails class="m-3" v-if="showVinylDetails && selectedVinyl" :vinyl="selectedVinyl" @closeDetails="actionCloseDetails"/>
        <ModifyForm class="m-3" v-if="showVinylModifyForm && selectedVinyl" :vinyl="selectedVinyl" @clickModify="actionClickModify"/>
      </div>
    </main>
</template>

<style scoped>
.bg-dark {
  min-height: 100vh;
}

</style>
