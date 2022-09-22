<script setup>
import Data from "@/assets/Data/Data.json"
import { ref } from "vue";
import List from "./List.vue";
const members = ref([]);
const assistants = ref([]);

function getGroupNames() {
	const groupNames = Data.map(person => person.group);
	const groups = [...new Set(groupNames)];
	return groups;
}

const groupNames = getGroupNames(); // grup isimleri bu değişkende tanımlı

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
const Group = ref(listedGroups.Group); // grup adı
const Assistant = ref(listedGroups.Assistant); //asistan adı
const Students = ref(listedGroups.Students); // öğrenciler 

</script>


<template>
	<div>
		<h1>Gruplar</h1>
		<ul>
			<li class="groups" v-for="groups in groupNames" @click="getSelectedGroup(groups)">{{groups}}</li>
		</ul>
		
		<List :Group="Group" :Students="Students" :Assistant="Assistant"/>
	</div>
	<!-- <template v-if="listedGroups">

		<h2 class="group">{{Group}}</h2>
		<ul>
			<li class="assistant" v-for="assistant in Assistant">{{assistant}}</li>
			<li class="student" v-for="student in Students">{{student}}</li>
		</ul>
		
	</template> -->
	
</template>

<style scoped>
.groups {
	cursor: pointer;
}

.assistant {
	background-color: aqua;
}
</style>