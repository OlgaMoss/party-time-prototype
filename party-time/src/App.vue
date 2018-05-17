
<template>
  <div id="app">
    <h1 class="ui dividing centered header">Vue.js Party App</h1>
    <div class='ui three column centered grid'>
      <div class='column'>
        <parties-list v-bind:parties="parties"></parties-list>
      </div>
    </div>
  </div>
</template>

<script>
import swal from 'sweetalert';
import PartiesList from './components/PartiesList';

export default {
  name: 'app',
  components: {
    PartiesList,
  },
  data() {
    return {
      parties: [{
        title: 'Party A',
        project: 'Project A',
        done: false,
      }, {
        title: 'Party B',
        project: 'Project B',
        done: true,
      }, {
        title: 'Party C',
        project: 'Project C',
        done: false,
      }, {
        title: 'Party D',
        project: 'Project D',
        done: false,
      }],
    };
  },
  methods: {
    createParty(newParty) {
      this.parties.push(newParty);
      swal('Success!', 'To-Do created!', 'success');
    },
  },
};
</script>
