<template>
  <q-page>
    <div class="q-pa-sm">
      <div class="row">
        <div class="col-12 col-sm-6 col-md-6" v-for="task in tasks" :key="task.id">
          <q-card :class="['q-my-xs', $q.screen.xs ? 'q-mx-none' : 'q-mx-xs']">
            <q-card-section class="q-pa-sm">
              <div class="row">
                <div class="text-subtitle1 text-bold">{{ task.title }}</div>
                <q-space />
                <q-icon name="delete" size="xs" color="primary" class="q-my-auto" @click="deleteTask(task.id)" />
              </div>
              <div class="flex q-pt-sm">
                <q-space />
                <div class="text-grey text-caption">{{ task.date }} {{ task.time }}</div>
              </div>
            </q-card-section>
          </q-card>
        </div>
      </div>
    </div>

  </q-page>
</template>

<script lang="ts">
import { Task } from 'src/models/task';
import { defineComponent, ref } from 'vue';

function useTask() {
  const tasks = ref([
    { id: 1, title: 'task1', date: '1401/10/12', time: '18:30' },
    { id: 2, title: 'task2', date: '1401/10/12', time: '19:50' }
  ] as Task[])

  /** deleteTask */
  function deleteTask(id: number) {
    var index = tasks.value.findIndex(t => t.id === id)
    if (index >= 0) {
      tasks.value.splice(index, 1)
    }
  }

  /** */
  return { tasks, deleteTask }
}

export default defineComponent({
  setup() {
    return { ...useTask() }
  }
});
</script>
