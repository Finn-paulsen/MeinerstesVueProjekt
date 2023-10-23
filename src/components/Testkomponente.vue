<template>

<h1>Wie lautet deine neue To-Do? {{props.props}}</h1>
</template> 

<script setup>

const props = defineProps(['props'])

console.log(props.props)

</script>

