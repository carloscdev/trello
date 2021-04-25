<template>
  <div class="task-view">
    <div class="flex flex-col flex-grow items-start justify-between px-4 w-full">
      <input
        type="text"
        class="p-2 mr-2 mb-3 block text-xl font-bold w-full"
        :value="task.name"
        @change="updateTaskProperty($event, 'name')"
        @keyup.enter="updateTaskProperty($event, 'name')"
      >
      
      <textarea
        clas="relative bg-transparent px-2 border mt-5 h-64 border-none leading-normal"
        :value="task.description"
        @change="updateTaskProperty($event, 'description')"
        @keyup.enter="updateTaskProperty($event, 'description')"
      />
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters(['getTask']),
    task () {
      return this.getTask(this.$route.params.id)
    }
  },
  methods: {
    updateTaskProperty(e, key) {
      this.$store.commit('UPDATE_TASK', {
        task: this.task,
        key,
        value: e.target.value
      })
    }
  }
}
</script>

<style>
.task-view {
  @apply relative flex flex-row bg-white pin mx-4 m-32 mx-auto py-4 text-left rounded shadow;
  max-width: 700px;
}
textarea:focus, input:focus {
  outline: 1px solid #38a89d;
}
textarea {
  min-width: 100%;
}
</style>
