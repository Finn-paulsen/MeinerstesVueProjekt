<template>

<h1>Hallo {{props.props}}</h1>
</template> 

<script setup>

const props = defineProps(['props'])

console.log(props.props)

</script>

