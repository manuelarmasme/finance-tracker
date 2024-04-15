<template>
  <div class="grid grid-cols-2 py-4 border-b border-gray-200 dark:border-gray-800 text-gray-900 dark:text-gray-100">
    <div class="flex justify-between items-center">
      <div class="flex items-center space-x-1">
        <UIcon :name="icon" :class="[iconColor]" />
        <div>{{ props.transaction.description }}</div>

        
      </div>

      <div><UBadge color="white" v-if="props.transaction.category"> {{ props.transaction.category }} </UBadge></div>
    </div>

    <div class="flex items-center justify-end space-x-2">
      <div>{{ currency }}</div>

      <UDropdown :items="items" :popper="{placement: 'bottom-start'}">
        <UButton color="white" variant="ghost" trailing-icon="i-heroicons-ellipsis-horizontal"/>

      </UDropdown>
    </div>
  </div>
</template>

<script setup>

const props = defineProps({
  transaction: Object
})

const {currency} = useCurrency(props.transaction.amount)

//checking the type of the income
const isIncome = computed(()=> props.transaction.type === 'Income')

//changing name icon with the type of the income
const icon = computed(()=> isIncome.value ? 'i-heroicons-arrow-up-right' : 'i-heroicons-arrow-down-left');

//chECKIN Icon color using the Income Type
const iconColor = computed(()=> isIncome.value ? 'text-green-600' : 'text-red-600');

const items = [[
  {
    label: 'Edit',
    icon: 'i-heroicons-pencil-square-20-solid',
    click: () => console.log('Edit')
  },
  {
    label: 'Delete',
    icon: 'i-heroicons-trash-20-solid',
    click: () => console.log('Delete')
  },
]]

</script>
