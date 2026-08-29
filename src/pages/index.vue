<template>
  <div>
    <p v-if="rocketStore.loading">Loading ....</p>
    <p v-else-if="rocketStore.error">
      Error: {{ rocketStore.error }}
      <button type="button" @click="rocketStore.fetchRockets">Retry</button>
    </p>
    <div v-else>
      <RouterLink v-for="rocket in rocketStore.rockets" :key="rocket.id" :to="`/rockets/${rocket.id}`"
        style="text-decoration: none; color: inherit;">
        <RocketCard :rocket="rocket" />

      </RouterLink>
    </div>

  </div>
</template>

<script lang="ts" setup>
import RocketCard from '@/components/RocketCard.vue';
import { onMounted } from 'vue';
import { useRocketStore } from '@/stores/rocket';

const rocketStore = useRocketStore();

onMounted(() => {
  rocketStore.fetchRockets();
});
</script>
