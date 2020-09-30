<template>
  <!-- :class →classListメソッド内で定義した定数名 -->
  <form :class="classList" @submit.prevent="addList">
    <input v-model="title"
        type="text"
        class="text-input"
        placeholder="Add new list"
        @focusin="startEditing"
        @focusout="finishEditing"
    >
    <button
        type="submit"
        class="add-button"
        v-if="isEditing || titleExists">
      Add
    </button>
  </form>
</template>

<script>
export default {
  data: function() {
    return {
      title: '',
      isEditing: false,
    }
  },
  computed: {
    classList() {
      // const 定数名 = class名
      const classList = ['addlist']
      if(this.isEditing) {
        // class="addlist"のフォームにclass="active"を付与する
        classList.push('active')
      }
      if(this.titleExists) {
        classList.push('addable')
      }
      return classList
    },
    titleExists() {
      return this.title.length > 0
    }
  },
  methods: {
    addList: function() {
      this.$store.dispatch('addlist', { title: this.title})
      this.title = ''
    },
    startEditing() {
      this.isEditing = true
    },
    finishEditing() {
      this.isEditing = false
    }
  }
}
</script>