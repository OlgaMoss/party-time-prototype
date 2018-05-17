<template>
  <div class='ui centered card'>
    <div class="content" v-show="!isEditing">
      <div class='header'>
          {{ party.title }}
      </div>
      <div class='meta'>
          {{ party.project }}
      </div>
      <div class='extra content'>
          <span class='right floated edit icon' v-on:click="showForm">
          <i class='edit icon'></i>
        </span>
        <span class='right floated trash icon' v-on:click="deleteParty(party)">
          <i class='trash icon'></i>
        </span>
      </div>
    </div>
    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>Title</label>
          <input type='text' v-model="party.title" >
        </div>
        <div class='field'>
          <label>Project</label>
          <input type='text' v-model="party.project" >
        </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' v-on:click="hideForm">
            Close X
          </button>
        </div>
      </div>
    </div>

  </div>
</template>

<script type="text/javascript">
export default {
  props: ['party'],
  data() {
    return {
      isEditing: false,
    };
  },
  methods: {
    deleteParty(party) {
      this.$emit('delete-party', party);
    },
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.isEditing = false;
    },
  },
};
</script>
