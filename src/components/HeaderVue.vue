<template>
    <div class="header">
        <p>{{ title }}</p>
    </div>
</template>
<script>
export default {
    data() {
        return {
            title: "Calculator",
        }
    },
}
</script>
<style scoped>
.header {
    margin: auto;
    width: 100px;
    text-align: center;
}
</style>