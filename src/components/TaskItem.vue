<template>
    <div class="task"><input type="checkbox" :checked="isCompleted">
        <p>{{ this.task }}</p>
        <button class="delete-task">×</button>
    </div>
</template>

<script>
export default {
    props: {
        task: {
            type: String,
            required: true,
        },
        isCompleted: {
            type: Boolean,
            required: true,
        }
    }
}
</script>

<style scoped></style>