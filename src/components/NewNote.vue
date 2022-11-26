<template>
  <div class="new-note">
		<label>Title</label>
    <input class="new-note__title" v-model="note.title" type="text" />
		<div class="new-note__priority">
			<p>Choose priority</p>
			<input v-model="note.priority" type="radio" name="priority" id="low" value="low" checked>
			<label for="low">low</label>

			<input v-model="note.priority" type="radio" name="priority" id="medium" value="medium">
			<label for="medium">medium</label>

			<input v-model="note.priority" type="radio" name="priority" id="high" value="high">
			<label for="high">high</label>
		</div>
		<label>Description</label>
    <textarea v-model="note.descr"></textarea>
    <button class="btn btnPrimary" @click="addNote">Add new note</button>
  </div>
</template>

<script>
export default {
	props: {
		note: {
			type: Object,
			required: true,
		},
		// priorities: {
		// 	type: Array,
		// 	required: true,
		// }
	},
	methods: {
		addNote() {
			this.$emit('addNewNote', this.note);
		}
	}
}
</script>

<style lang="scss">
.new-note {
	text-align: center;
	margin-bottom: 40px;
	&__title, textarea {
		font-family: 'Montserrat', sans-serif;
	}

	// new-note__priority (radio-button)
	&__priority {
		margin-bottom: 26px;

		&>p {
			margin-bottom: 15px;
			font-weight: 700;
		}

		input[type="radio"] {
			display: none;
		}

		label {
			display: inline-block;
			padding: 5px 15px;
			cursor: pointer;
			border: 1px solid #303133;
			border-radius: 20px;
			margin-bottom: 0;
			transition: all .3s ease;
		}

		label + input + label {
			margin-left: 15px;
		}

		input[type="radio"]:checked+label,
		label:hover {
			background: #9a9a9a;
			color: #fff;
		}
	}
}
</style>