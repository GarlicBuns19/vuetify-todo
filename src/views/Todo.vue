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
      @click:append="addTask(), taskAdded()"
      @keyup.enter="addTask()"
    ></v-text-field>
    <div v-if="tasks">
      <div v-for="task in tasks" :key="task.id">
        <v-list class="pt-0" flat data-aos="fade-down">
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
                <v-dialog v-model="dialog" persistent max-width="600px">
                  <template v-slot:activator="{ on, attrs }">
                    <v-btn
                      icon
                      v-bind="attrs"
                      v-on="on"
                    >
                      <v-icon color="primary lighten-1"
                        >mdi-circle-edit-outline</v-icon
                      >
                    </v-btn>
                  </template>
                  <v-card>
                    <v-card-text>
                      <v-container>
                        <v-row>
                          <v-col cols="12" sm="6" md="4">
                            <v-text-field
                              label="Edit this task to"
                              v-model="task.title"
                            ></v-text-field>
                          </v-col>
                        </v-row>
                      </v-container>
                    </v-card-text>
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn color="blue darken-1" text @click="dialog = false">
                        Close
                      </v-btn>
                      <v-btn
                        color="blue darken-1"
                        @click="editTodo(task.id)"
                        text
                      >
                        Edit
                      </v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
              </v-list-item-action>
              <v-list-item-action>
                <v-btn @click="deleteTodo(task.id), taskDel()" icon>
                  <v-icon color="primary lighten-1">mdi-delete</v-icon>
                </v-btn>
              </v-list-item-action>
            </template>
          </v-list-item>
        </v-list>
        <v-divider></v-divider>
      </div>
    </div>
    <center>
      <h1 data-aos="fade-up" id="tAdd">Task added</h1>
    </center>
    <center>
      <h1 data-aos="fade-up" id="tDel">Task Deleted</h1>
    </center>
    <div v-if="tasks == ''" class="text-center">
      <div class="mt-16">
        <h3 class="display-1">No tasks</h3>
        <v-icon class="black--text">mdi-sticker-check-outline</v-icon>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      dialog : false ,
      newTask: "",
      tasks: [
        {
          id: 1,
          title: `dwaodaiodhawidhawiodhawiodhaidhaiu`,
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
      let newTask = {
        id: this.tasks.length + 1,
        title: `${this.newTask}`,
        done: false,
      };
      if (this.tasks == "") {
        this.tasks = [];
      }
      this.tasks.push(newTask);
      this.newTask = "";
    },
    deleteTodo(id) {
      console.log(id);
      this.tasks = this.tasks.filter((t) => t.id !== id);
    },
    editTodo(id) {
      console.log("This task has just been edited");
      this.dialog = false;
    },
    taskAdded() {
      var x = document.getElementById("tAdd");
      if ((x.style.display = "none")) {
        x.style.display = "block";
      }
      if ((x.style.display = "block")) {
        setTimeout(function gone() {
          x.style.display = "none";
        }, 1000);
      }
    },
    taskDel() {
      var x = document.getElementById("tDel");
      if ((x.style.display = "none")) {
        x.style.display = "block";
      }
      if ((x.style.display = "block")) {
        setTimeout(function gone() {
          x.style.display = "none";
        }, 1000);
      }
    },
  },
};
</script>

<style scoped>
#tAdd {
  display: none;
}
#tDel {
  display: none;
}
</style>


