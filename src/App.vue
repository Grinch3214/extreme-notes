<template>
  <div class="wrapper">

    <div class="wrapper-content">
      <section>
        <div class="container">
          <h1 class="main-title">{{ title }}</h1>
					<message-vue v-if="message" :message="message" />
					<new-note :note="note" @addNewNote="addNote" />
					<notes-vue :notes="notes" @removeItem="removeNote" />
				</div>
      </section>
    </div>

  </div>
</template>

<script>
import MessageVue from "./components/MessageVue.vue";
import NewNote from './components/NewNote.vue';
import NotesVue from './components/NotesVue.vue';

export default {
  name: 'App',
  components: {
		MessageVue,
    NewNote,
    NotesVue,
  },
	data:() => ({
		title: 'Extreme notes',
		message: null,
		note: {
			title: '',
			descr: ''
		},
		notes: [
			{
				title: 'First note',
				descr: 'Description for first note',
				date: new Date(Date.now()).toLocaleString()
			},
			{
				title: 'Second note',
				descr: 'Description for second note',
				date: new Date(Date.now()).toLocaleString()
			},
			{
				title: 'Last note',
				descr: 'Description for last note',
				date: new Date(Date.now()).toLocaleString()
			},
		],
	}),
	methods: {
		addNote() {
			let { title, descr } = this.note;

			if (title === '') {
				this.message = 'Title can`t be blank'
				return false
			}

			this.notes.push({
				title,
				descr,
				date: new Date(Date.now()).toLocaleString()
			});

			this.message = null;
			this.note.title = '',
			this.note.descr = ''
		},
		removeNote(index) {
			this.notes.splice(index, 1);
		}
	},
}
</script>

<style lang="scss">
.main-title {
	font-size: 36px;
	text-align: center;
	margin-bottom: 40px;
	letter-spacing: 2.5px;
}
</style>
