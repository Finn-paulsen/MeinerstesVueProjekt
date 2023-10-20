<template>

<h1>Hallo, ich habe Hunger. Bitte füttere mich mit neuen ToDos, wenn du diese abschließt bin ich dazu nicht nur satt sondern auch glücklich. {{props.props}}</h1>
</template> 

<script setup>

const props = defineProps(['props'])

console.log(props.props)

</script>

