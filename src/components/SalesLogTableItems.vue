<template>
    <DataTable v-model:expandedRows="expandedSalesLogOrderItemComponents" :value="props.items">
        <Column expander style="width: 5rem" />
        <Column sortable field="ItemName" :header="$t('name')"></Column>
        <Column sortable field="Cost" :header="$t('cost')"></Column>
        <Column sortable field="Quantity" :header="$t('quantity')">
            <template #body="slotProps">
                <div>{{ slotProps.data.Quantity != "0" ? slotProps.data.Quantity : "1" }}</div>
            </template></Column>
        <Column sortable field="SalePrice" :header="$t('sale_price')"></Column>
        <Column sortable field="profit" :header="$t('profit')">
            <template #body="slotProps">
                <div :style="`${ (slotProps.data.SalePrice - slotProps.data.Cost) > 0 ? 'color:green' : 'color:red' }`">{{ slotProps.data.SalePrice - slotProps.data.Cost }}</div>
            </template>
        </Column>
        <template #expansion="slotProps">
            <DataTable :value="slotProps.data.Components">
                <Column sortable field="ComponentName" :header="$t('name')"></Column>
                <Column sortable field="Cost" :header="$t('cost')"></Column>
                <Column sortable field="Quantity" :header="$t('quantity')"></Column>
                <Column sortable field="EntryId" :header="$t('entry')"></Column>
            </DataTable>
            <SalesLogTableItems v-if="slotProps.data.DownstreamCost != null" :items="slotProps.data.DownstreamCost" />    
        </template>
    </DataTable>
</template>

<script setup lang="ts">

import {defineProps,ref} from 'vue'
import DataTable from 'primevue/datatable'
import Column from 'primevue/column'

const props = defineProps(['items'])
const expandedSalesLogOrderItemComponents = ref([])
</script>