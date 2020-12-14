<template>
    <div>
        <v-container v-if="isMobile" >
            <div :key="todo.id" v-for="todo in todoList">
                <TodoItem :todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
            </div>
        </v-container>
        <v-container fluid v-else>
            <v-row dense>
            <v-col
            :key="todo.id" v-for="todo in todoList"
                cols="4"
            >
                <TodoItem :todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>            
            </v-col>
            </v-row>
        </v-container>
    </div>    
</template>

<script>

import TodoItem from './TodoItem'

export default {
    name: "Todos",
    components: {
        TodoItem
    },
    props: ["todoList"],
    computed: {
        isMobile: () => {
            if(/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)) {
                return true
            } else {
                return false
            }
        }
    }
}
</script>
