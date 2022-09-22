<script setup>
const props = defineProps(["persons", "groupName"]);

</script>

<template>
	<h2>{{props.groupName}}</h2>
	<div class="container">
		<div :class="person.type==null ? 'student':'assistant', person.group " v-for="person in props.persons" class="card">
			<div class="card-header">
				<p>{{person.name}}</p>
			</div>
			<div class="card-body">
				<p>{{person.type==null ? "Student":"Assistant"}}</p>
			</div>
		</div>

	</div>
</template>

<style scoped>
.Orchid {
	border: 3px solid orchid;
}

.Orchid.assistant {
	background-color: orchid;
}


.SteelBlue {
	border: 3px solid steelblue;
}

.SteelBlue.assistant {
	background-color: steelblue;
}


.IndianRed {
	border: 3px solid IndianRed;
}

.IndianRed.assistant {
	background-color: IndianRed;
}


.YellowGreen {
	border: 3px solid YellowGreen;
}

.YellowGreen.assistant {
	background-color: YellowGreen;
}


.LightSeaGreen {
	border: 3px solid LightSeaGreen;
}

.LightSeaGreen.assistant {
	background-color: LightSeaGreen;
}



.container {
	display: grid;
	gap: 24px;
	grid-template-columns: repeat(3, 1fr);
}
</style>