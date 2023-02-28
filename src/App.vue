<template>
    <div class="common-layout">
        <el-container class="main">
            <el-header class="main__header">
                <img src="/pink_platypus.png" class="main__header--img" />
                <a
                    href="https://github.com/Sonatai/todo-vue-ts"
                    target="_blank"
                    class="main__header__link"
                    >Git Repo</a
                ></el-header
            >
            <el-main class="container">
                <div>
                    <button @click="addListItem">add list</button>
                </div>
                <div v-if="getAllListsItems().length > 0" class="main__content">
                    <TodoList
                        v-for="item in getAllListsItems()"
                        :id="item.id"
                        :key="item"
                        :todoItems="item.todoItems"
                        :name="item.name"
                    />
                </div>
            </el-main>
        </el-container>
    </div>
</template>

<script lang="ts">
import 'element-plus/dist/index.css';
import { nanoid } from 'nanoid';
import './components/TodoList/TodoList.vue';
import './style.scss';

export default {
    methods: {
        getAllListsItems(): any[] {
            const arr: any[] = [];
            const localStorageObj = { ...localStorage };
            Object.keys(localStorageObj).forEach((key) =>
                arr.push(JSON.parse(localStorageObj[key]))
            );

            return arr;
        },
        addListItem(): void {
            const emptyList = {
                id: nanoid().toString(),
                name: '',
                todoItems: [],
            };
            localStorage.setItem(emptyList.id, JSON.stringify(emptyList));

            // TODO: Meh, this is bad. Research how to do it better later maybe
            // Have a look at Vuex.
            location.reload();
        },
    },
};
</script>
