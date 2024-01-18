<script setup>
import axios from "axios";
import { ref, onBeforeMount, computed } from "vue";


const url = ref(`https://fakestoreapi.com/products`);


const number = ref(0);
const filter = ref("");
const rows = ref([]);
const columns = [
  { name: 'id', label: 'ID', align: 'left', field: 'id', sortable: true },
  { name: 'title', label: 'Title', align: 'left', field: 'title', sortable: true },
  { name: 'price', label: 'Price', align: 'left', field: 'price', sortable: true },
  { name: 'description', label: 'Description', align: 'left', field: 'description', sortable: true },
  { name: 'category', label: 'Category', align: 'left', field: 'category', sortable: true },
  { name: 'price', label: 'Price', align: 'left', field: 'price', sortable: true }
];
const initialPagination = {
  rowsPerPage: 10
}

const getData = async (url) => {
  try {
    const { data } = await axios.get(url);
    rows.value = data
    return data;
  } catch (error) {
    console.log(error);
  };
};

const option = ref(
  {
    label: "asc",
    value: 1
  }
);
const options = [
  {
    label: "asc",
    value: 1
  },
  {
    label: "desc",
    value: 0
  },
];


const urlOptions = computed(async () => {
  if (option.value.value == 1) {
    url.value = "https://fakestoreapi.com/products?sort=asc"
    await getData(url.value)
  } else {
    url.value = "https://fakestoreapi.com/products?sort=desc"
    await getData(url.value)
  }
})


const numberUrl = async () => {
  if (number.value <= 0) {
    url.value = `https://fakestoreapi.com/products?limit=10`
    await getData(url.value)
  } else {
    url.value = `https://fakestoreapi.com/products?limit=${number.value}`
    await getData(url.value)
  }
}


onBeforeMount(async () => {
  await getData(url.value);
});

</script>

<template>
  <q-page class="q-pa-xl text-center">
    <q-input type="number" outlined v-model="number" @click="numberUrl()">
      <q-icon name="pin" />
    </q-input>
    <q-select class="q-mt-md" outlined v-model="option" :options="options" @click="urlOptions"
      label="Elige una opción"></q-select>

    <q-table class="q-mt-md" :grid="$q.screen.xs" flat bordered title="Producs" :pagination="initialPagination"
      :filter="filter" :rows="rows" :columns="columns" row-key="name">
      <template v-slot:top-right>
        <q-input color="black" v-model="filter" placeholder="Buscar">
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input>
      </template>
    </q-table>
  </q-page>
</template>

