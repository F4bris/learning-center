<script setup>
import {useI18n} from "vue-i18n";
import {useRoute, useRouter} from "vue-router";
import usePublishingStore from "../../aplication/publishing.store.js";
import {computed, onMounted, ref} from "vue";
import {Category} from "../../domain/model/category.entity.js";

const {t} = useI18n();

const route = useRoute();

const router = useRouter();
const store = usePublishingStore();
const {errors, addCategory, updateCategory} = store();
const  form = ref({name : ''});
const isEdit = computed(() => !!route.params.id);

onMounted(() => {
  console.log(route.params.id);
  if(isEdit.value){
    const category = getCategoryById(route.params.id);
    console.log(category);
    if(category) form.value.name = category.name;
    else router.push({name: 'publishing-category', params: {id: route.params.id
  }
});

function getCategoryById(id) {
  return store.getCategoryById(id);
}

const saveCategory = () => {
  const category = new Category({id: isEdit.value? route.params.id : null, name: form.value.name,});
  if(isEdit.value) updateCategory(category); else addCategory(category);
  navigatetoback;
}

</script>

<template>

</template>

<style scoped>

</style>