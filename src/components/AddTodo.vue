<template>
  <div>
    <v-btn 
      x-large
      block
      @click="expandForm = !expandForm"
    >     
      Add Todo
    </v-btn>
    
    <v-expand-transition>
      <v-card
        v-show="expandForm"
      >
       <v-row
        class="mb-6"
        no-gutters
      >

        <v-text-field 
        label="Type here" 
        v-model="title" 
        :disabled="loadingAddTodo"
        ></v-text-field>
        <v-btn
          class="mx-2"
          fab
          small
          bottom
          :disabled="loadingAddTodo"
          :loading="loadingAddTodo"
          color="primary"
          @click="addTodo"
        >
          <v-icon dark>
            mdi-plus
          </v-icon>
        </v-btn>
      </v-row>     
      </v-card>      
    </v-expand-transition>
    
  </div>
</template>

<script>

import { v4 as uuidv4 } from 'uuid';

export default {
  name: "AddTodo",
  data() {
    return{
      title: '',
      expandForm: false,
      loadingAddTodo: false
    }  
  },
  methods: {
    async addTodo() {
      this.loadingAddTodo = true;
      const imageURL = await this.getRandomImage();
      
      const newTodo = {
        id: uuidv4(),
        title: this.title,
        completed: false,
        color: "white",
        confirmDelete: false,
        image: imageURL
      };

      this.$emit('add-todo', newTodo);
      this.title = "";
      this.expandForm = false;
      this.loadingAddTodo = false;
    },
    async getRandomImage() {
      try {
        const { url, status } = await fetch('https://picsum.photos/200/300');
        console.log("status" , status);
        if(status != 200) {
          throw new TypeError()
        }
        return url;
      } catch (error) {
        console.log("Failed to fetch a random image :(");
        return require('../assets/logo.png');
      }
      
    }
  }
}
</script>