<template>
  <section class="flex items-center justify-between mb-10">
    <h1 class="text-4xl font-extrabold">Summary</h1>
    <div>
      <USelectMenu v-model="selectedView" :options="transactionsViewOptions" />
    </div>
  </section>
</template>

<script setup>
import {transactionsViewOptions} from '../constants'

const selectedView = ref(transactionsViewOptions[1]);
</script>
