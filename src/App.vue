<template>
    <div class="common-layout">
        <el-container class="main">
            <el-header class="main__header">Header</el-header>
            <el-main>
                <button @click="addListItem">add list</button>
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
import TodoList from './components/TodoList/TodoList.vue';
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
                todoItems: [
                    { value: false, label: 'Woap Woap' },
                    { value: false, label: 'Woap Woap' },
                    { value: false, label: 'Woap Woap' },
                    { value: false, label: 'Woap Woap' },
                    { value: false, label: 'Woap Woap' },
                    { value: false, label: 'Woap Woap' },
                    { value: false, label: 'Woap Woap' },
                ],
            };
            localStorage.setItem(emptyList.id, JSON.stringify(emptyList));

            // TODO: Meh, this is bad. Research how to do it better later maybe
            // Have a look at Vuex.
            location.reload();
        },
    },
};
</script>
