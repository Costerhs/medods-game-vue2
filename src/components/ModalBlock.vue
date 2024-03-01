<template>
    <div class="modal" v-if="modalStatus">
        <p> Вы проиграли!</p>
        <p>Раундов сыграно: {{ rounds - 1 }}</p>
        <button @click="$emit('restart')">Попробовать снова!</button>
    </div>
</template>

<script>
    export default {
        props:['rounds','modalStatus']
    }
</script>

<style scoped>

</style>