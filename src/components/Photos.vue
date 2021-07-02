<template>
<div class="temp-photos">
  <h1>Photos</h1>
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
import { useRoute } from "vue-router";
import Loader from "./Loader";

export default {
    components: {
        Loader,
    },
    setup() {
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

        return { list, isLoading };
    }
}
</script>

<style>
.temp-photos{
    background-color: white;
    padding: 5px;
    border-radius: 1rem;
}
.div-photos {
  display: flex;
  align-items: center;
  border: 1px solid lightgray;
  border-radius: 0.2rem;
  margin: 1rem;
}
.div-photos img{
    padding: 5px;
}
</style>