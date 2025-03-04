<template>
  <Dialog
    v-model="showDialog"
    class="z-50"
    :options="{
      title: 'Sold T-shirt Details',
    }"
    role="dialog"
    aria-modal="true"
    aria-labelledby="dialog-title"
    aria-describedby="dialog-description"
  >
    <template #body-content>
      <div class="text-sm">
        <h2 id="dialog-title" tabindex="-1">Sold T-shirt Details</h2>
        <p id="dialog-description" class="mb-2">T-shirts sold for this event.</p>
      </div>
      <table class="w-3/4 table-fixed text-center" role="table" aria-describedby="dialog-title">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50">
          <tr role="row">
            <th class="p-2 border" role="columnheader" scope="col">Size</th>
            <th class="p-2 border" role="columnheader" scope="col">Quantity</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(quantity, size) in insight.tshirt_size_count" :key="size" role="row">
            <td class="p-2 text-base border" role="cell">{{ size }}</td>
            <td class="p-2 text-base border" role="cell">{{ quantity }}</td>
          </tr>
          <tr role="row">
            <td class="p-2 text-base font-semibold" role="rowheader">Total</td>
            <td class="p-2 text-base font-semibold" role="cell">{{ insight.tshirts_sold }}</td>
          </tr>
        </tbody>
      </table>
      <!-- Accessible Close Button -->
      <button
        class="absolute top-4 right-4 p-2 focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
        @click="showDialog = false"
        aria-label="Close dialog"
        title="Close dialog"
      >
        <svg aria-hidden="true" class="w-6 h-6">...</svg>
      </button>
    </template>
  </Dialog>

  <div class="flex flex-col w-full border rounded-sm p-4">
    <div class="text-sm flex gap-2 items-center uppercase font-semibold">
      <IconShirtFilled class="w-5 h-5" aria-hidden="true" />
      <h3> T-shirts Sold </h3>
    </div>
    <div class="flex gap-2 items-end justify-between mt-6">
      <div class="prose">
        <h3 id="total-tshirts" class="text-lg font-bold">{{ insight.tshirts_sold }}</h3>
      </div>
      <button 
        id="view-details-btn"
        class="w-fit inline-flex items-center justify-center gap-2 transition-colors focus:outline-none 
               focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 hover:bg-gray-100 active:bg-gray-200"
        @click="showDialog = true"
        role="button"
        aria-labelledby="dialog-title view-details-btn"
        aria-describedby="button-description"
        aria-label="View sold T-shirt details"
        title="View sold T-shirt details"
      >
        <span>View Details</span>
      </button>
      <p id="button-description" class="sr-only">Opens a dialog with T-shirt sales details.</p>
    </div>
  </div>
</template>

<script setup>
import { Dialog } from 'frappe-ui'
import { defineProps, ref, watch, nextTick } from 'vue'
import { IconShirtFilled } from '@tabler/icons-vue'

const showDialog = ref(false)

const props = defineProps({
  insight: {
    type: Object,
    required: true,
  },
})

// Manage focus when dialog opens
watch(showDialog, (newValue) => {
  if (newValue) {
    nextTick(() => {
      document.getElementById("dialog-title").focus();
    });
  }
})
</script>
