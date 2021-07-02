<template>
<div class="temp-photos">
  <h1>Photos</h1>
  <button @click="back" class="btn-voltar">Back</button>
  <loader v-if="isLoading" />
  <div class="div-photos" v-for="(photo, index) in list" :key="index">
      <img :src="photo.thumbnailUrl">
      {{ photo.title }}
  </div>
</div>
</template>

<script>
import { onMounted, ref } from "vue";
import { getPhotos } from "../service/photos-service.js";
import { useRouter, useRoute } from "vue-router";
import Loader from "./Loader";

export default {
    components: {
        Loader,
    },
    setup() {
        const router = useRouter();
        const route = useRoute();
        const list = ref(null);
        const isLoading = ref(false);

        onMounted(() => {
             isLoading.value = true;
            getPhotos(route.params.id).then(resp => {
                list.value = resp;
            }).finally(() => {
                isLoading.value = false;
            });
        })

        const back = () => router.replace("/");

        return { list, isLoading, back };
    }
}
</script>

<style>
.temp-photos{
    background-color: rgb(236, 236, 236);
    padding: 5px;
    border-radius: 1rem;
}
.div-photos {
  display: flex;
  align-items: center;
  background: white;
  border: 1px solid lightgray;
  border-radius: 0.2rem;
  margin: 1rem;
}
.div-photos img{
    padding: 5px;
}
.btn-voltar {
  background-color: #0e6af3;
  border: none;
  border-radius: 5px;
  color: white;
  padding: 10px 27px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 15px;
  margin: 8px;
}
</style>