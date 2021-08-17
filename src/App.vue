<template>
	<h1>Vue 3 Todo App</h1>
	<form @submit.prevent="addNewTodo">
		<label>List of Todo's</label>
		<input v-model="newTodo" name="newTodo" />
		<button>Add New</button>
	</form>

	<button @click="markAllDone">Mark All</button>

	<button @click="removeAll">Remove All</button>

	<div v-for="(todo, index) in todos" :key="todo.id" id="todo">
		<h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
			{{ todo.content }}
		</h3>
		<button @click="removeTodo(index)">Remove Todo</button>
	</div>
</template>

<script>
import { ref } from "vue";

export default {
	setup() {
		const newTodo = ref("");
		const todos = ref([]);

		function addNewTodo() {
			console.log(newTodo.value);

			todos.value.push({
				id: Date.now(),
				done: false,
				content: newTodo.value,
			});
			newTodo.value = "";
		}

		function toggleDone(todo) {
			todo.done = !todo.done;
		}

		function removeTodo(index) {
			todos.value.splice(index, 1);
		}

		function markAllDone() {
			todos.value.forEach((todo) => (todo.done = true));
		}

		function removeAll() {
			todos.value = [];
		}

		return {
			todos,
			newTodo,
			addNewTodo,
			toggleDone,
			removeTodo,
			markAllDone,
			removeAll,
		};
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}

body {
	font-family: sans-serif;
	padding-top: 1em;
	padding-bottom: 1em;
	font-size: 1.3em;
	width: 40%;
	margin: 0 auto;
}

input,
textarea,
button,
p,
div,
section,
article,
select {
	display: block;
	width: 100%;
	font-family: sans-serif;
	font-size: 1em;
	margin: 0.5em;
}

#todo {
	cursor: pointer;
}

.done {
	text-decoration: line-through;
}
</style>
