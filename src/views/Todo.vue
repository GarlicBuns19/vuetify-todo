<template>
  <section class="todoMain pa-6">
    <v-text-field
      v-model="newTask"
      class="pa-3"
      outlined
      label="Add task"
      append-icon="mdi-message-plus-outline"
      hide-details
      clearable
      @click:append="addTask()"
      @keyup.enter="addTask()"
    ></v-text-field>
    <div v-if="tasks">
      <div v-for="task in tasks" :key="task.id">
        <v-list class="pt-0" flat>
          <v-list-item :class="{ 'blue lighten-5': task.done }">
            <template v-slot:default>
              <v-list-item-action>
                <v-checkbox
                  :input-value="task.done"
                  @click="todoDone(task.id)"
                  color:primary
                ></v-checkbox>
              </v-list-item-action>

              <v-list-item-content>
                <v-list-item-title
                  :class="{ 'text-decoration-line-through': task.done }"
                  >{{ task.title }}</v-list-item-title
                >
              </v-list-item-content>
              <v-list-item-action>
                <v-btn @click="deleteTodo(task.id)" icon>
                  <v-icon color="primary lighten-1">mdi-delete</v-icon>
                </v-btn>
              </v-list-item-action>
            </template>
          </v-list-item>
        </v-list>
        <v-divider></v-divider>
      </div>
    </div>
    <div v-else>Nothing tfgvbhjnmk</div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
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
    addTask() {
      let newTask = this.newTask;
      this.tasks.push({
        id: this.tasks.length + 1,
        title: `${newTask}`,
        done: false,
      });
      this.newTask = "";
    },
    deleteTodo(id) {
      console.log(id);
      this.tasks = this.tasks.filter((t) => t.id !== id);
    },
  },
};
</script>
