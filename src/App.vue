<script setup>
import Data from "@/assets/Data/Data.json";
import { ref, onMounted } from "vue";
import GroupList from "./components/GroupList.vue";
import PersonsList from "./components/PersonsList.vue";

const groupNames = ref([]);
const Members = ref([]);
const groupName = ref("");

onMounted(() => {	//onMount olduğunda çalıştırdım
	getGroups(Data);
})

const getGroups = async (data) => {	// grup isimlerini unique hale getirdiğim fonksiyon
	const groups = await data.map(person => person.group);
	const uniqueGroupNames = [...new Set(groups)];
	groupNames.value = uniqueGroupNames;
}

const getGroupPersons = (GroupName) => {	//grup isimlerini aldığım fonksiyon
	Members.value = Data.filter(person => person.group === GroupName);
	if (Members.value.length > 0) {	//filtrelenmiş verinin kontrolü
		groupName.value = GroupName;
	}
}

</script>

<template>
	<GroupList :groupNames="groupNames" @getGroupPersons="getGroupPersons" />
	<PersonsList :persons="Members" :groupName="groupName" />
</template> 

<style scoped>

</style>
