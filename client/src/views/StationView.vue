<template>
  <div class="about">
    <el-page-header @back="goBack">
      <template #content>
        {{stationData?.prices[0].station}}
      </template>

      <el-table :data="stationData?.prices" stripe style="width: 100%">
        <el-table-column prop="updatedAt"
                         label="Date"
                         width="180">
          <template #default="scope">{{ new Date(scope.row.updatedAt).toLocaleString() }}</template>
        </el-table-column>
        <el-table-column prop="e10" label="E10" width="180" />
        <el-table-column prop="super" label="Super" />
        <el-table-column prop="diesel" label="Diesel" />
      </el-table>
    </el-page-header>
  </div>
</template>

<style>
</style>
<script setup>
import { onMounted, ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import { getGasStation } from '@/api/services/main.service.js';

const route = useRoute();
const router = useRouter();
const stationData = ref(null);

const getStation = async () => {
  const result = await getGasStation(route.params.id);
  stationData.value = result.data;
};

onMounted(async () => {
  await getStation();
});

const goBack = () => {
  router.back()
};
</script>