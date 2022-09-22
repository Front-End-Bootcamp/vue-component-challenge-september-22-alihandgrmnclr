<script setup>
const props = defineProps(["Group","Assistant","Students"]);
const groupName = props.Group;
const Assistant = props.Assistant;
const Students = props.Students;

</script>

<template>
	<h3>{{groupName}}</h3>
	<ul>
		<li v-for="student in Students"> {{student}} </li>
	</ul>
</template>

<style>

</style>