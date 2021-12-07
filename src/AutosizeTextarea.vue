<template>
    <textarea v-bind="$attrs"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"/>
</template>

<script>
export default {
    name: 'AutosizeTextarea',

    props: {
        modelValue: {
            type: String,
            required: true,
        },
    },

    emits: ['update:modelValue'],

    mounted() {
        this.resize();
        this.$el.style['overflow-y'] = 'hidden';

        this.$el.addEventListener('input', this.resize);
    },

    beforeUnmount() {
        this.$el.removeEventListener('input', this.resize);
    },

    methods: {
        resize(event = null) {
            const el = event ? event.target : this.$el;

            el.style.height = 'auto';
            el.style.height = `${el.scrollHeight}px`;
        },
    },
};
</script>
