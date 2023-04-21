<template>
    <header>
        <h1>{{ title }}</h1>
        <Button @btn-click="$emit('toggle-add-task')"
        :text="showAddTask ? 'Close' : 'New Task'" 
        :color="showAddTask ? 'red' : 'green'"/> <!-- adding as props -->
    </header>
</template>

<script>
import Button from './Button'

export default {
    name: 'Header',
    props: {
        title: String,
        showAddTask: Boolean,
    },
    components: {
        Button,
        }
}
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>