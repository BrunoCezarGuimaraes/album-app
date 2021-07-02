<template>
<div class="temp-album">
  <h1>Albums</h1>
  <loader v-if="isLoading"/>
  <div
    class="div-album"
    v-for="(album, index) in list"
    :key="index"
    @click="selectAlbum(album.id)"
  >
    {{ album.title }}
  </div>
</div>
</template>

<script>
import { onMounted, ref } from "vue";
import { getAlbumsList } from "../service/photos-service.js";
import { useRouter } from "vue-router";
import Loader from "./Loader";

export default {
    components: {
    Loader
  },
  setup() {
    const list = ref([]);
    const router = useRouter();
    const isLoading = ref(false);

    onMounted(() => {
        isLoading.value = true;
      getAlbumsList().then((resp) => {
        list.value = resp;
      }).finally(() => {
          isLoading.value = false;
      });
    });

    const selectAlbum = (id) => {
      router.push({ name: "photos", params: { id } });
    };

    return { list, selectAlbum, isLoading };
  },
};
</script>

<style>
.temp-album{
    background-color: white;
    padding: 5px;
    width: 23rem;
    border-radius: 1rem;
}
.div-album {
  display: flex;
  align-items: center;
  border: 1px solid lightgray;
  border-radius: 0.2rem;
  margin: 0.5rem;
  cursor: pointer;
}
</style>