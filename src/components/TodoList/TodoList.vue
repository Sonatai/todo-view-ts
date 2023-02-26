<template>
    <el-form :model="form" label-width="120px">
        <el-card class="box-card card">
            <div class="card-header card__header">
                <el-input
                    v-model="form.name"
                    @change="() => updateList(form)"
                />
                <el-button class="button" text @click="deleteList(form)">
                    Delete
                </el-button>
            </div>
            <div class="card__body">
                <TodoItem
                    v-for="todoItem in form.todoItems"
                    :key="todoItem"
                    :value="todoItem.value"
                    :label="todoItem.label"
                    :id="form.id"
                />
            </div> </el-card
    ></el-form>
</template>

<script lang="ts">
import './styles.scss';
import { reactive } from 'vue';
import TodoItem from '../TodoItem/TodoItem.vue';

interface IProp {
    name: string;
    id: string;
    todoItems: {
        label: string;
        value: boolean;
    }[];
}

export default {
    props: {
        name: {
            type: String,
            required: true,
        },
        id: {
            type: String,
            required: true,
        },
        todoItems: {
            type: Array<{
                label: string;
                value: boolean;
            }>,
            required: true,
        },
    },
    setup: (props: IProp): any => {
        const form = reactive({
            name: props.name,
            id: props.id,
            todoItems: props.todoItems,
        });

        return {
            form,
        };
    },
    methods: {
        updateList(props: IProp): void {
            localStorage.setItem(props.id, JSON.stringify(props));
        },
        deleteList(props: IProp): void {
            localStorage.removeItem(props.id);

            // TODO: Meh, this is bad. Research how to do it better later maybe
            // Have a look at Vuex.
            location.reload();
        },
    },
};
</script>
