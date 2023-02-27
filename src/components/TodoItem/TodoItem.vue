<template>
    <div class="text item todo-item">
        <input
            v-model="props.value"
            type="checkbox"
            class="todo-item__checkbox"
        />
        <input v-model="props.label" type="text" @change="updateItem(props)" />
    </div>
</template>

<script lang="ts">
import './styles.scss';

interface IProp {
    label: string;
    value: boolean;
    id: string;
    index: number;
}

export default {
    props: {
        label: {
            type: String,
            required: true,
        },
        value: {
            type: Boolean,
            required: true,
        },
        id: {
            type: String,
            required: true,
        },
        index: {
            type: Number,
            required: true,
        },
    },
    setup: (props: IProp): any => {
        return { props };
    },
    methods: {
        updateItem(props: IProp): void {
            const item = localStorage.getItem(props.id);
            if (item) {
                const itemObj = JSON.parse(item);
                itemObj.todoItems[props.index].label = props.label;
                itemObj.todoItems[props.index].value = props.value;

                localStorage.setItem(props.id, JSON.stringify(itemObj));
            }
        },
    },
};
</script>
