<template>
    <div id="task-list">
        <p id="start-message" v-if="tasks.length === 0">Немає завдань</p>
        <TaskItem @deleteTask="editTasks" @changeCompleted="updateCompleted" v-for="task in tasks" :key="task.id"
            :id="task.id" :task="task.taskName" :isCompleted="task.isCompleted">
        </TaskItem>
    </div>
</template>

<script>
import TaskItem from '@/components/TaskItem.vue';

export default {
    components: { TaskItem },
    props: {
        tasks: {
            type: Array,
            required: true,
        },
    },
    methods: {
        updateCompleted(id) {
            this.$emit('editData', id);
        },
        editTasks(id) {
            this.$emit('delete', id);
        }
    }
}
</script>

<style scoped></style>