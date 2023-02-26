<template>
    <div class="text item todo-item">
        <input
            v-model="props.value"
            type="checkbox"
            class="todo-item__checkbox"
        />
        <input v-model="props.label" type="text" />
    </div>
</template>

<script lang="ts">
import './styles.scss';

interface IProp {
    label: string;
    value: boolean;
    id: string;
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
    },
    setup: (props: IProp): any => {
        return { props };
    },
};
</script>
