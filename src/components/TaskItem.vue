<template>
    <div class="task" :class="{ 'completed': this.isCompleted === true }">
        <input type="checkbox" :checked="isCompleted" @change="changeCompleted">
        <p>{{ this.task }}</p>
        <button class="delete-task" @click="deleteTask">×</button>
    </div>
</template>

<script>
export default {
    props: {
        id: {
            type: Number,
            required: true
        },
        task: {
            type: String,
            required: true,
        },
        isCompleted: {
            type: Boolean,
            required: true,
        }
    },
    methods: {
        changeCompleted() {
            this.$emit('changeCompleted', this.id);
        },
        deleteTask() {
            this.$emit('deleteTask', this.id);
        }
    }
}
</script>

<style scoped></style>