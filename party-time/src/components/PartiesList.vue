<template>
  <div>
    <p class="tasks">
      Completed Tasks:
      {{parties.filter(party => {return party.done === true}).length}}</p>
    <p class="tasks">
      Pending Tasks:
      {{parties.filter(party => {return party.done === false}).length}}</p>
    <party v-on:delete-party="deleteParty"
     v-for="party in parties"
     :key="party.id" :party.sync="party"></party>
  </div>
</template>

<script type = "text/javascript" >
import swal from 'sweetalert';
import Party from './Party';

export default {
  props: ['parties'],
  components: {
    Party,
  },
  methods: {
    deleteParty(party) {
      swal(
        {
          title: 'Are you sure?',
          text: 'This To-Do will be permanently deleted!',
          icon: 'warning',
          buttons: true,
          dangerMode: true,
        })
        .then((willDelete) => {
          if (willDelete) {
            const partyIndex = this.parties.indexOf(party);
            this.parties.splice(partyIndex, 1);
            swal('Deleted!', 'Your To-Do has been deleted.', 'success');
          } else {
            swal('Your imaginary file is safe!');
          }
        });
      // ,
      // () => {
      //   const partyIndex = this.parties.indexOf(party);
      //   this.parties.splice(partyIndex, 1);
      //   swal('Deleted!', 'Your To-Do has been deleted.', 'success');
      // },
    },
    // completeParty(party) {
    //   const partyIndex = this.parties.indexOf(party);
    //   this.parties[partyIndex].done = true;
    //   swal('Success!', 'To-Do completed!', 'success');
    // },
  },
};
</script>

<style scoped>
  p.tasks {
    text-align: center;
  }
</style>
