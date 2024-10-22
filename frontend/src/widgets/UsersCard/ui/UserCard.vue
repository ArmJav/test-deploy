<script setup lang="ts">

import { reactive, ref } from 'vue';
import type { UnwrapRef } from 'vue';

const columns = [
  {
    title: 'ФИО',
    dataIndex: 'name',
    width: '25vw',
  },
  {
    title: 'Дата рождения',
    dataIndex: 'birthday',
    width: '40vw',
  },
  {
    title: 'Статус',
    dataIndex: 'status',
    width: '40vw',
  },
  {
    title: 'Операции',
    dataIndex: 'operation',
  },
];
interface DataItem {
  key: string;
  name: string;
  birthday: string;
  status: string;
}
const data: DataItem[] = [
  {
    "key": "0a749c6e-2b6e-4231-8f37-5f3d2094a289",
    "name": "Anna Smith",
    "birthday": "1995-05-25",
    "status": "Single"
  },
  {
    "key": "9e13271f-4790-4736-aed1-167291972377",
    "name": "John Doe",
    "birthday": "1975-03-12",
    "status": "Married"
  },
  {
    "key": "7642889c-3290-4790-971f-638271f4736a",
    "name": "Sarah Johnson",
    "birthday": "1980-09-18",
    "status": "Divorced"
  },
  {
    "key": "12903271f-4790-4736-aed1-167291972377",
    "name": "Emma Watson",
    "birthday": "1990-04-15",
    "status": "In a relationship"
  },
  {
    "key": "47903271f-4790-4736-aed1-167291972377",
    "name": "Tom Hardy",
    "birthday": "1980-07-03",
    "status": "Single"
  },
  {
    "key": "903271f4-7903-271f-4736-aed167291972",
    "name": "Brad Pitt",
    "birthday": "1963-12-18",
    "status": "Married"
  },
  {
    "key": "3271f479-0327-1f47-36ae-d16729197237",
    "name": "Angelina Jolie",
    "birthday": "1975-06-04",
    "status": "Divorced"
  },
  {
    "key": "71f47903-271f-4736-aed1-67291972377",
    "name": "Jennifer Aniston",
    "birthday": "1962-02-11",
    "status": "Single"
  },
  {
    "key": "47903271-f479-0327-1f47-36ae67291972",
    "name": "Adam Sandler",
    "birthday": "1962-09-09",
    "status": "Married"
  },
  {
    "key": "1f479032-71f4-7903-271f-4736ae67291",
    "name": "Drew Barrymore",
    "birthday": "1975-02-22",
    "status": "Divorced"
  },
  {
    "key": "47903271-f479-0327-1f47-36ae6729197",
    "name": "Matt Damon",
    "birthday": "1970-10-08",
    "status": "Single"
  }];
// for (let i = 0; i < 15; i++) {
//   data.push({
//     key: i.toString(),
//     name: `Edrward ${i}`,
//     birthday: '21.08.1999',
//     status: `London Park no. ${i}`,
//   });
// }

const dataSource = ref(data);
const editableData: UnwrapRef<Record<string, DataItem>> = reactive({});

const value_search = ref<string>('');
const onSearch = (searchValue: string) => {
  console.log('use value', searchValue);
  console.log('or use this.value', value_search.value);
};

</script>

<template>

    <div class="conteiner">
    <a-input-search
      v-model:value="value_search"
      placeholder="Поиск"
      style="width: 70%"
      @search="onSearch"
      class = "mb-3"
        />
    <a-table :columns="columns" :data-source="dataSource" bordered>
        <template #bodyCell="{ column, text, record }">
        <template v-if="['ФИО', 'Дата рождения', 'Статус'].includes(column.dataIndex)">
            <div>
            <a-input
                v-if="editableData[record.key]"
                style="margin: -5px 0"
            />
            <template v-else>
                {{ text }}
            </template>
            </div>
        </template>
        <template v-else-if="column.dataIndex === 'operation'">
            <div class="editable-row-operations">
            <span v-if="editableData[record.key]">
            </span>
            <span v-else>
                <a >Посмотреть</a>
            </span>
            </div>
        </template>
        </template>
    </a-table>
    </div>

</template>


<style scoped >
    .conteiner {
        width: 100vw;
        align-items: center;
        padding: 10px;
        margin: 5vh;
    }
</style>
