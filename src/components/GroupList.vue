<script setup>
const props = defineProps(["groupNames"]);
const emits = defineEmits(["getGroupPersons"]);

const getMembers = (groupName) => {
	emits('getGroupPersons', groupName);
}
</script>

<template>
	<ul>
		<li class="groups" v-for="group in props.groupNames" @click="getMembers(group)">{{group}}</li>
	</ul>

</template>

<style scoped>
.groups {
	cursor: pointer;
}
</style>