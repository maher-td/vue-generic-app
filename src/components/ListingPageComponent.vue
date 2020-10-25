<!-- Needed NPM Installs -->
<!-- npm i axios vue-multiselect v-calendar@1.0.0 -->

<template>
    <section class="generic-listing">
        <div class="generic-date-picker filter-selector">
          <div class="container">
              <div class="content">
                <div class="date-picker">                
                  <v-date-picker :masks="{  weekdays: 'WWW', L: 'DD MMM YYYY' }" :input-props='{placeholder: "التاريخ", readonly: true}' transition="none" ref="datePicker" :step="1" :from-date="new Date(2020, 0, 1)" :popover="{ placement: 'bottom', visibility: 'click' }"  mode="range" v-model='selectedDate' :columns="1" />
                </div>
                <button class="btn btn-danger" v-on:click="clearDate">X</button>
                <div class="generic-list-filter">
                  <multiselect v-model="dropdownValue" :options="dropdownData" placeholder="Pick a value"></multiselect>
                </div>
              </div>
          </div>
      </div>
      <div class="container">
        <div class="row">
          <div class="col-md-4 mb-4" :key="index" v-for="(item , index) in genericData">
            <div class="card">
              <a :href="item.url">
                <img class="card-img-top" :src="item.thumbnailUrl" alt="Card image cap">
              </a>
              <div class="card-body">
                <a :href="item.url">
                  <h5 class="card-title">{{item.id}}</h5>
                </a>
                <p class="card-text">{{item.title}}</p>
                <a :href="item.url" class="btn btn-primary">ShowMore</a>
              </div>
            </div>
          </div>
        </div>
        <div class="generic-error-msg" v-show="showNoDataMessage">
            <div class="icon">
                <i class="icon-inbox"></i>
            </div>
            <p class="error-title">EmptyListMessagelbl</p>
            <a v-bind:href="goHome"><i class="icon-home"></i>HomePagelbl</a>
        </div>
        <div class="listing-loader" v-show="isAjaxLoading">
            <img src="../../src/assets/spinner.gif" />
        </div>
      </div>

      <div class="observer"></div>
    </section>
</template>

<style lang="scss">
    @import './src/assets/sass/ListingPageComponent';
</style>

<script>

import DatePicker from 'v-calendar/lib/components/date-picker.umd'
import Multiselect from 'vue-multiselect'
import axios from 'axios'
import Vue from 'vue';

Vue.component('v-date-picker', DatePicker)

let listingThis;
let contactApiUrl;

export default {
    components: {
      Multiselect
    },
    data: function() { 
        return {
            genericData: [],
            scrollCount: 1,
            showNoDataMessage: true,
            isAjaxLoading: false,
            isthierMoreData: true,
            goHome: '',
            selectedDate: {
            start: null,
            end: null
            },
            dropdownData: ['all', 'past', 'current', 'upcoming'],
            dropdownValue: '',
        }
    },
      methods: {
     getData: function () {
       
      listingThis.isAjaxLoading = true;

      // concatApiUrl = `${apiUrl}/api/EventsListAPI?nodePath=${this.nodePath}&culture=${this.currentLanguage}&eventType=${this.dropdownValue}&dateFrom=${dateFromVal}&dateTo=${dateToVal}&pageNumber=${this.scrollCount}`

      contactApiUrl = `https://jsonplaceholder.typicode.com/photos?albumId=${listingThis.scrollCount}`

      axios.get(contactApiUrl)
          .then(function (response) {
              if (response.data != "") {
                listingThis.showNoDataMessage = false;
                  if (listingThis.scrollCount == 1) {
                    listingThis.genericData = response.data;
                  } else {
                    listingThis.genericData = listingThis.genericData.concat(response.data);
                  }
              } else {
                listingThis.isthierMoreData = false;

                  //check if scroll count == 1 so i can show empty message

                  if (listingThis.scrollCount == 1) {
                    listingThis.genericData = [];
                    listingThis.showNoDataMessage = true;
                  }
              }
              listingThis.isAjaxLoading = false;

          })
      //TODO Probably will need to make our dates disabled till load
    },
    changeUrlParams: function (paramValue) {
      let queryParams = new URLSearchParams(window.location.search);      
      if (paramValue == listingThis.dropdownValue) {
        queryParams.delete("category");
        queryParams.set("category", paramValue);
      } else {
        queryParams.delete("start-date");
        queryParams.set("start-date", listingThis.selectedDate.start);
        queryParams.delete("end-date");
        queryParams.set("end-date", listingThis.selectedDate.end);
      }
      history.replaceState(null, null, "?" + queryParams.toString());
    },
    getUrlParams: function () {
      const queryString = window.location.search;
      const urlParams = new URLSearchParams(queryString);
      const start_date = urlParams.get('start-date');
      const end_date = urlParams.get('end-date');
      const category = urlParams.get('category');
      listingThis.selectedDate = {
        start: new Date(start_date),
        end: new Date(end_date)
      }
      listingThis.dropdownValue = category;

      let dropdownItems = document.querySelectorAll('.dropdown-item');
      dropdownItems.forEach((item) => {
        if(category == item.value) {
          item.checked = true;
        }
      })
    },
    clearDate: function () {
      listingThis.selectedDate = {
        start: null,
        end: null
      }
    }
  },
  computed: {},
  watch: {
    'selectedDate.start': function () {
      listingThis.changeUrlParams(listingThis.selectedDate.start)
      listingThis.getData();
    },
    'selectedDate.end': function () {
      listingThis.changeUrlParams(listingThis.selectedDate.end)
    },
    dropdownValue: function () {
      if(listingThis.dropdownValue != null) {
        listingThis.changeUrlParams(listingThis.dropdownValue)
      }
      listingThis.scrollCount = 1;
      listingThis.isthierMoreData = true;
      listingThis.getData();
    }
  },
  mounted() {
    listingThis = this;

    listingThis.getUrlParams(); 
    
    listingThis.getData();

    let observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting && !listingThis.isAjaxLoading && listingThis.isthierMoreData) {
          listingThis.scrollCount++;
          listingThis.getData();
        }
      });
    });

    //this is make cause footer content is loaded late so it's positions changed
    setTimeout(function () {
        const container = document.querySelector(".observer");
        observer.observe(container);
    }, 100);
  }
}
</script>