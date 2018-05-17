
<template>
  <div class='ui basic content center aligned segment'>
      <div class="content left aligned">
        <ul class="ui list">
            <li v-for="category in categories" :key="category.id" :category.sync="category">
                {{category.name}}
                <span class='right floated edit icon' v-on:click="showForm">
                    <i class='edit icon'></i>
                </span>
                <span class='right floated trash icon' v-on:click="deleteCategory(category)">
                    <i class='trash icon'></i>
                </span>
                <div class="content" v-show="isEditing">
                    <div class='ui form'>
                        <div class='field'>
                            <label>Название</label>
                            <input type='text' v-model="category.name" >
                        </div>
                        <div class='ui two button attached buttons'>
                            <button class='ui basic blue button' v-on:click="hideForm">
                                Close X
                            </button>
                        </div>
                    </div>
                </div>
            </li>
        </ul>
      </div>
    <button class='ui basic button icon' v-on:click="openForm" v-show="!isCreating">
      <i class='plus icon'></i>
    </button>
    <div class='ui centered card' v-show="isCreating">
      <div class='content left aligned'>
        <div class='ui form'>
          <div class='field'>
            <label>Название новой категории</label>
            <input v-model="nameText" type='text'>
          </div>
          <div class='ui two button attached buttons'>
            <button class='ui basic blue button' v-on:click="sendForm()">
              Create
            </button>
            <button class='ui basic red button' v-on:click="closeForm">
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import swal from 'sweetalert';

export default {
  data() {
    return {
      categories: [{
        name: 'Концерт',
      }, {
        name: 'Квартирник',
      }, {
        name: 'Клубная вечеринка',
      }],
      nameText: '',
      isCreating: false,
      isEditing: false,
    };
  },
  methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
    },
    deleteCategory(category) {
      swal(
        {
          title: 'Are you sure?',
          text: 'This party will be permanently deleted!',
          icon: 'warning',
          buttons: true,
          dangerMode: true,
        })
        .then((willDelete) => {
          if (willDelete) {
            const categoryIndex = this.categories.indexOf(category);
            this.categories.splice(categoryIndex, 1);
            swal('Deleted!', 'Your category has been deleted.', 'success');
          } else {
            swal('Your imaginary file is safe!');
          }
        });
    },
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.isEditing = false;
    },
    sendForm() {
      if (this.nameText.length > 0) {
        const name = this.nameText;
        this.categories.push({ name });
        this.nameText = '';
        this.isCreating = false;
      }
    },
  },
};
</script>
