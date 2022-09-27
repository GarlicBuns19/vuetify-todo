<template>
  <section class="todoMain pa-6">
    <div v-for="task in tasks" :key="task.id">
      <v-list class="pt-0" flat>
        <v-list-item 
        @click="todoDone(task.id)" 
        :class="{ 'blue lighten-5' : task.done}">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color:primary></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
              :class="{'text-decoration-line-through' : task.done}"
              >{{ task.title }}</v-list-item-title>
            </v-list-item-content>
          </template>
        </v-list-item>
      </v-list>
      <v-divider></v-divider>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: "Eat Food",
          done: false,
        },
        {
          id: 2,
          title: "Milk",
          done: false,
        },
        {
          id: 3,
          title: "Car",
          done: false,
        },
      ],
    };
  },
  methods: {
    todoDone(id) {
      let task = this.tasks.filter((t) => t.id === id)[0];
      task.done = !task.done;
    },
  },
};
</script>
