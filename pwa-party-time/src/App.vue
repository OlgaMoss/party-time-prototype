
<template>
  <div id="app">
    <h1 class="ui dividing centered header">Vue.js Party App</h1>
    <div class="ui two item menu">
      <a class="item active" v-on:click="showForm">Вечеринки</a>
      <a class="item" v-on:click="hideForm">Категории</a>
    </div>
    <div class='ui one column centered grid'>
      <div class='column'>
        <parties-list v-bind:parties="parties" v-show="isSelectedParties"></parties-list>
        <create-party v-on:create-party="createParty" v-show="isSelectedParties"></create-party>
        <category v-show="!isSelectedParties"></category>
      </div>
    </div>
  </div>
</template>

<script>
import swal from 'sweetalert';
import $ from 'jquery';
import PartiesList from './components/PartiesList';
import CreateParty from './components/CreateParty';
import Category from './components/Category';


export default {
  name: 'app',
  components: {
    PartiesList,
    CreateParty,
    Category,
  },
  data() {
    return {
      isSelectedParties: true,
      categories: [{
        name: 'Концерт',
      }, {
        name: 'Квартирник',
      }, {
        name: 'Клубная вечеринка',
      }],
      parties: [{
        name: 'Вечеринка A',
        description: 'Описание A',
        isFreeEntry: false,
        date: '2015-10-02',
        time: '13:30',
        price: 500,
        address: 'Адрес А',
        category: 'Квартирник',
      }, {
        name: 'Вечеринка B',
        description: 'Описание B',
        isFreeEntry: true,
        date: '2015-10-02',
        time: '13:30',
        price: 500,
        address: 'Адрес B',
        category: 'Квартирник',
      }, {
        name: 'Вечеринка C',
        description: 'Описание C',
        isFreeEntry: false,
        date: '2015-10-02',
        time: '13:30',
        price: 500,
        address: 'Адрес C',
        category: 'Квартирник',
      }, {
        name: 'Вечеринка D',
        description: 'Описание D',
        isFreeEntry: false,
        date: '2015-10-02',
        time: '13:30',
        price: 500,
        address: 'Адрес D',
        category: 'Квартирник',
      }],
    };
  },
  methods: {
    createParty(newParty) {
      this.parties.push(newParty);
      swal('Success!', 'Party created!', 'success');
    },
    showForm() {
      this.isSelectedParties = true;
    },
    hideForm() {
      this.isSelectedParties = false;
    },
  },
  mounted() {
    $.getJSON('data/data.json', (parties) => {
      this.parties = parties;
    });
  },
  created() {
    this.$emit('get-categories', this.categories);
  },
};
</script>

<style>
 @media screen and (min-device-width: 1200px) and (max-device-width: 1600px) and (-webkit-min-device-pixel-ratio: 1) {
    /* .column{
        /* widows:; */
  /* } */
 }
/* landscape */
 @media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: landscape) {
 }
 /* portrait */
@media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: portrait) {
}
/* landscape */
@media only screen and (min-device-width: 320px) and (max-device-width: 736px) and (orientation: landscape) {
}
/* portrait */
@media only screen and (min-device-width: 320px) and (max-device-width: 736px) and (orientation: portrait) {
}
</style>
