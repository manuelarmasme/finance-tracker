<template>
  <section class="flex items-center justify-between mb-10">
    <h1 class="text-4xl font-extrabold">Summary</h1>
    <div>
      <USelectMenu v-model="selectedView" :options="transactionsViewOptions" />
    </div>
  </section>

  <section
    class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 sm:gap-16 mb-10"
  >
    <Trend
      color="green"
      title="Income"
      :amount="4000"
      :last-amount="3000"
      :loading="false"
    />
    <Trend
      color="red"
      title="Expense"
      :amount="4000"
      :last-amount="5000"
      :loading="false"
    />
    <Trend
      color="green"
      title="Investments"
      :amount="4000"
      :last-amount="3000"
      :loading="false"
    />
    <Trend
      color="red"
      title="Saving"
      :amount="4000"
      :last-amount="4100"
      :loading="false"
    />
  </section>

  <section>
    <Transaction
      v-for="transaction in transactions"
      :key="transaction.id"
      :transaction="transaction"
    />
  </section>
</template>

<script setup>
import { transactionsViewOptions } from "../constants";

const selectedView = ref(transactionsViewOptions[1]);

const supabase = useSupabaseClient();

const transactions = ref([]);

// useAsyncData leds that I only do the fect data into the server and not in the client

const { data, pending } = await useAsyncData("transactions", async () => {
  const { data, error } = await supabase.from("transactions").select();

  if (error) return []

  return data
});

//to get data
transactions.value = data.value;
</script>
