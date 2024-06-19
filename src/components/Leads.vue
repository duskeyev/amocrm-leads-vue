<template>
  <div>
    <a-input-search
        v-model:value="query"
        placeholder="Поиск сделок"
        @input="filterLeads"
        enter-button
    />
    <a-table :columns="columns" :dataSource="filteredLeads" row-key="id" />
  </div>
</template>

<script lang="ts">
import {defineComponent, ref, onMounted, resolveComponent} from 'vue';
import axios from 'axios';
import {format} from "date-fns";
import moment from 'moment'

export default defineComponent({
  name: 'Leads',
  setup() {
    const query = ref('');
    const leads = ref([]);
    const filteredLeads = ref([]);
    const columns = [
      { title: 'Название', dataIndex: 'name', key: 'name' },
      { title: 'Бюджет', dataIndex: 'price', key: 'price' },
      { title: 'Статус', dataIndex: 'status_name', key: 'status_name' },
      { title: 'Ответственный', dataIndex: 'owner', key: 'owner' },
      { title: 'Дата создания', dataIndex: 'created_at', key: 'created_at'
      },
    ];

    const fetchLeads = async () => {
      const response = await axios.get('/api/leads');
      console.log(response.data)
      leads.value = response.data.map((lead: any) => ({
        ...lead,
        created_at:  moment.unix(lead.created_at).format('YYYY-MM-DD HH:mm:ss'),

      }));
      filteredLeads.value = leads.value;

    };

    const filterLeads = () => {
      const lowerCaseQuery = query.value.toLowerCase();
      filteredLeads.value = leads.value.filter((lead: { name: string }) =>
          lead.name.toLowerCase().includes(lowerCaseQuery)
      );
    };

    onMounted(fetchLeads);

    return {
      query,
      leads,
      filteredLeads,
      columns,
      fetchLeads,
      filterLeads,
    };
  },
});
</script>

<style scoped>

 </style>
