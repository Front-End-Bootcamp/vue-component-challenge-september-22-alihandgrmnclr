<script setup>
import Data from "@/components/Data/Data.json"
import { ref } from "vue";
const members = ref([]);
const assistants = ref([]);

function getGroupList() {
	const groupNames = Data.map(person => person.group);
	const groups = [...new Set(groupNames)];
	return groups;
}

const groupNames = getGroupList(); // grup isimleri bu değişkende tanımlı

function filterByGroupName(GroupName) {
	const check = Data.some(Data => Data.group == GroupName);	// grup adının var olup olmadığının kontrolü
	if (check) {
		const filteredMembers = Data.filter(member => member.group == GroupName && member.type == null);	// grup adına göre filtreleme işlemleri
		const filteredAssistant = Data.filter(assistant => assistant.group == GroupName && assistant.type != null);

		members.value = filteredMembers.map(members => members.name);
		assistants.value = filteredAssistant.map(assistants => assistants.name);

		return {	// geriye obje döndürüyorum
			Group: GroupName,
			Assistant: assistants.value,
			Students: members.value
		}

	} else {
		return alert("Hatali grup adı")
	}
}

function getSelectedGroup(groupName = "Orchid") { // default olarak Orchid grubunu verdim
	console.log(groupName);
	return groupName;
}
const selectedGroup = getSelectedGroup();

const listedGroups = filterByGroupName(selectedGroup);
const Group = ref(listedGroups.Group); //listedGroups.Group;
const Assistant = ref(listedGroups.Assistant);
const Students = ref(listedGroups.Students);

</script>


<template>
	<div>
		<ul>
			<li class="groups" v-for="groups in groupNames" @click="getSelectedGroup(groups)">{{groups}}</li>
		</ul>
	</div>
	<template v-if="listedGroups">

		<h2 class="group">{{Group}}</h2>
		<ul>
			<li class="assistant" v-for="assistant in Assistant">{{assistant}}</li>
			<li class="student" v-for="student in Students">{{student}}</li>
		</ul>

	</template>


</template>

<style scoped>
.groups {
	cursor: pointer;
}

.assistant {
	background-color: aqua;
}
</style>