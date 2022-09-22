<script setup>
import Data from "@/assets/Data/Data.json";
import { ref, onMounted } from "vue";
import GroupList from "./components/GroupList.vue";
import PersonsList from "./components/PersonsList.vue";
const groupNames = ref([]);
const Members = ref([]);
const groupName = ref(null);

const getGroups = async (data) => {
	const groups = await data.map(person => person.group);
	const uniqueGroups = [...new Set(groups)];
	groupNames.value = uniqueGroups;
}

const getGroupPersons = (GroupName) => {
	Members.value = Data.filter(person => person.group === GroupName);
	groupName.value = GroupName;
}

onMounted(() => {
	getGroups(Data);
})

</script>

<template>
	<GroupList :groupNames="groupNames" @getGroupPersons="getGroupPersons" />
	<PersonsList :persons="Members" :groupName="groupName"/>
</template> 

<style scoped>

</style>
