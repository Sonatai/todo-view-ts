<template>
    <el-form :model="form" label-width="120px">
        <el-card class="box-card card">
            <div class="card-header card__header">
                <el-input
                    v-model="form.name"
                    @change="() => updateList(form)"
                />
                <el-button class="button" text @click="deleteList(form.id)">
                    X
                </el-button>
            </div>
            <div class="card__body">
                <div v-if="form.todoItems.length > 0">
                    <!-- Meh doesnt work, dunno why. Maybe ref isn't pass down or something like this :( -->
                    <!-- <TodoItem
                        v-for="(todoItem, index) in form.todoItems"
                        :key="index"
                        :value="todoItem.value"
                        :label="todoItem.label"
                        :id="form.id"
                    /> -->
                    <div
                        v-for="(todoItem, index) in form.todoItems"
                        :key="index"
                        class="text item todo-item"
                    >
                        <!-- $event has a wrong type. Real value has a checked ~> so I cast it as any for this example 😶 -->
                        <input
                            v-model="todoItem.value"
                            type="checkbox"
                            class="todo-item__checkbox"
                            @click="
                                ($event) =>
                                    updateCheckbox(
                                        form.id,
                                        index,
                                        ($event.target as any).checked
                                    )
                            "
                        />
                        <input
                            v-model="todoItem.label"
                            type="text"
                            @change="
                                updateLabel(form.id, index, todoItem.label)
                            "
                        />
                        <button @click="deleteItem(form.id, index)">X</button>
                    </div>
                </div>
                <button @click="addItem(form)">Add Todo</button>
            </div>
        </el-card></el-form
    >
</template>

<script lang="ts">
import './styles.scss';
import { reactive } from 'vue';

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
        deleteList(id: string): void {
            localStorage.removeItem(id);

            // TODO: Meh, this is bad. Research how to do it better later maybe
            // Have a look at Vuex.
            location.reload();
        },
        addItem(props: IProp): void {
            props.todoItems.push({
                label: '',
                value: false,
            });

            localStorage.setItem(props.id, JSON.stringify(props));
        },
        updateLabel(id: string, index: number, value: string): void {
            const list = localStorage.getItem(id);
            if (list) {
                const listObj = JSON.parse(list);
                listObj.todoItems[index].label = value;

                localStorage.setItem(id, JSON.stringify(listObj));
            }
        },
        updateCheckbox(id: string, index: number, value: boolean): void {
            const list = localStorage.getItem(id);
            if (list) {
                const listObj = JSON.parse(list);
                listObj.todoItems[index].value = value;

                localStorage.setItem(id, JSON.stringify(listObj));
            }
        },
        deleteItem(id: string, index: number): void {
            const list = localStorage.getItem(id);

            if (list) {
                const listObj = JSON.parse(list);
                listObj.todoItems.splice(index, 1);
                localStorage.setItem(id, JSON.stringify(listObj));

                // TODO: Meh, this is bad. Research how to do it better later maybe
                // Have a look at Vuex.
                location.reload();
            }
        },
    },
};
</script>
