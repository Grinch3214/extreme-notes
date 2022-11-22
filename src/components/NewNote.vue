<template>
  <div class="new-note">
		<label>Title</label>
    <input class="new-note__title" v-model="note.title" type="text" />
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
		}
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
	&__title, textarea {
		font-family: 'Montserrat', sans-serif;
	}
}
</style>