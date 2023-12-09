<template>
    <div id="task-list">
        <transition name="fade">
            <p id="start-message" v-if="tasks.length === 0">Немає завдань</p>
        </transition>
        <transition-group name="list">
            <TaskItem @deleteTask="editTasks" @changeCompleted="updateCompleted" v-for="task in tasks" :key="task.id"
                :id="task.id" :task="task.taskName" :isCompleted="task.isCompleted">
            </TaskItem>
        </transition-group>
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

<style scoped>
.list-item {
    display: inline-block;
    margin-right: 10px;
}

.list-enter-active,
.list-leave-active {
    transition: all 0.5s;
}

.list-enter-from,
.list-leave-to {
    opacity: 0;
    transform: translateX(30px);
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity .5s;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>