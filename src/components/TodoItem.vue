
<template>
  <v-card
    max-width="400"
    class="mx-auto"
  >
    <v-container>
      <v-row dense>
        <v-col
          cols="12"
        >
          <v-card
            :color="todo.color"
          >
            <div class="d-flex flex-no-wrap justify-space-between">
              <div>
                <v-card-title
                  class="headline"
                  v-text="todo.title"
                ></v-card-title>
                <v-card-actions>
                  <v-btn
                    class="ml-2 mt-5"
                    outlined
                    rounded
                    small
                    color="green"
                    @click="markComplte"
                  >
                    Done!
                  </v-btn>
                  <v-btn  
                    v-if="!todo.confirmDelete"               
                    class="ml-2 mt-5"
                    outlined
                    rounded
                    small
                    @click="requestDeleteTodo"
                  >
                    Remove
                  </v-btn>
                  <v-btn
                    v-else                
                    class="ml-2 mt-5"
                    outlined
                    rounded
                    small
                    color="red"
                    @click="$emit('del-todo', todo.id)"
                  >
                    Confirm
                  </v-btn>
                </v-card-actions>
              </div>
              <v-avatar
                class="ma-3"
                size="125"
                tile
              >
                <v-img :src="todo.image"></v-img>
              </v-avatar>
            </div>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todo"],
    data: () => ({
      
    }),
    methods: {
        markComplte() {
            console.log("marked complete!!!");
            this.todo.completed = !this.todo.completed;
            this.todo.color = this.todo.color == "#d5eb34" ? "#ffffff" : "#d5eb34";
            this.todo.confirmDelete = false;
        },
        requestDeleteTodo() {
            console.log("request delete")
            this.todo.color = "#ffb3b3";
            this.todo.confirmDelete = true;
        }
    }
}    
</script>