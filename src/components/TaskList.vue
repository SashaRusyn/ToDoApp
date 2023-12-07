<template>
    <div id="task-list">
        <p id="start-message">Немає завдань</p>
        <TaskItem v-for="task in tasks" :task="task.taskName" :isCompleted="task.isCompleted"></TaskItem>
    </div>
</template>

<script>
import TaskItem from '@/components/TaskItem.vue';

export default {
    props: {
        tasks: {
            type: Array,
            required: true,
        },
    },
    components: { TaskItem },
}
</script>

<style scoped></style>