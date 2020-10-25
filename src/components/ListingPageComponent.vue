<template>
    <section class="generic-listing">
        <div class="generic-date-picker filter-selector">
          <div class="container">
              <div class="content">
                <div class="date-picker">                
                  <v-date-picker :masks="{  weekdays: 'WWW', L: 'DD MMM YYYY' }" :input-props='{placeholder: "التاريخ", readonly: true}' transition="none" ref="datePicker" :step="1" :from-date="new Date(2020, 0, 1)" :popover="{ placement: 'bottom', visibility: 'click' }"  mode="range" v-model='selectedDate' :columns="1" />
                </div>
                <span class="reset-date bg-white" v-on:click="clearDate">X</span>
                  <div class="generic-list-filter">
                      <multiselect v-model="dropdownValue" :options="dropdownData" placeholder="Pick a value"></multiselect>
                  </div>
              </div>
          </div>
      </div>
      <div class="container">
        <div class="row">
          <div class="col-md-4 mb-4" :key="index" v-for="(item , index) in genericData">
            <div class="generic-card">
              <div class="card-img">
                <a :href="item.url">
                  <img :src="item.thumbnailUrl" />
                </a>
              </div>
              <a :href="item.url">
                <h4 class="title">{{item.id}}</h4>
              </a>
              <p class="description">{{item.title}}</p>
              <a :href="item.url" class="read-more">ShowMore</a>
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
            <!-- <img src="../../../../src/assets/spinner.gif" /> -->
        </div>
      </div>

      <div class="observer"></div>
    </section>
</template>

<style lang="scss">
    $start: left;
    $end: right;

    .generic-listing {
  padding: 0 0 60px;

  .date-picker-container {
    position: relative;

    .icon-close-screen {
      position: absolute;
      top: 0;
      #{$end}: 60px;
      z-index: 1;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;

      &:before {
        color: #822726;
        font-size: 13px;
        cursor: pointer;
      }
    }
  }

  .generic-date-picker {
    display: block;
    margin: auto;
    margin: 60px 0;
    background-color: #6e0002;
    padding: 15px 0;

    .content {
      display: flex;
      justify-content: center;

      .date-picker {
        width: 260px;
        background-color: #fff;
        cursor: pointer;

        input {
          padding: 14px 20px !important;
          width: 260px;
          border: 0;
          cursor: pointer;

          &:focus {
            border: 0 !important;
          }
        }

        .vc-popover-content {
          margin: 0;
          border-radius: 0;
          .vc-popover-caret {
            display: none;
          }
        }
      }

      .generic-list-filter {
        display: none;
      }

      .reset-date {
        width: 50px;
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
        background-color: #ffffff;
      }
    }
  }

  .filter-selector {
    .content {
      justify-content: space-between;

      .vdp-datepicker {
        margin: 0;
        height: 50px;
      }

      .generic-list-filter {
        display: block;

        .multiselect__select {
          display: none;
        }

        .multiselect__tags {
          width: 260px;
          border-radius: 0;
          padding: 13px;
          cursor: pointer;

          .multiselect__single,
          .multiselect__input {
            margin-bottom: 0;
          }
        }
        .multiselect__content-wrapper {
          .multiselect__option--selected,
          .multiselect__option--highlight {
              background: #f3f3f3;
              color: #35495e;          
          }
          .multiselect__option--selected,
          .multiselect__option--highlight {
            &:after {
              display: none;
            }
          }
        }
      }
    }
  }

  .listing-loader {
    display: block;
    text-align: center;
    background-color: #ffffff;
  }
}

    .generic-card {
  box-shadow: 0 3px 6px 0 rgba(0, 0, 0, 0.16);
  border: solid 1px #c1b6b6;
  padding: 25px;
  margin-bottom: 30px;
  height: 100%;

  a {
      text-decoration: none !important;
  }

  .card-img {
      position: relative;
      margin-bottom: 10px;
      background-color: #f3f3f3;
      display: flex;
      justify-content: center;

      &:before {
          display: block;
          content: "";
          width: 100%;
          padding-top: (208 / 303) * 100%;
          background-color: #f3f3f3;
      }

      a {
          width: 100%;
          height: 100%;
          display: flex;
          align-items: center;
          justify-content: center;
          position: absolute;
          top: 0;
          #{$start}: 0;
      }

      img {
          /*position: absolute;
              top: 0;
              #{$start}: 0;
              bottom: 0;
              #{$end}: 0;*/
          max-width: 100%;
          max-height: 100%;
      }
  }

  a {
      .title {
          font-size: calc(var(--a) * calc(14px + (18 - 14) * ((100vw - 768px) / (1920 - 768))));
          font-family: "CR";
          font-weight: bold;
          color: #6e0002;
          margin-bottom: 15px;
      }
  }

  .description {
      color: #000000;
      font-size: calc(var(--a) * calc(14px + (18 - 14) * ((100vw - 768px) / (1920 - 768))));
  }

  .read-more {
      font-size: calc(var(--a) * 13px);
      font-weight: bold;
      color: #6e0002;
      text-align: $start;
  }
    }

    .generic-error-msg {
        padding: 60px 0 100px;
        text-align: center;
        display: block;
        margin: auto;

        .icon {
            margin-bottom: 30px;

            i {
                &:before {
                    font-size: calc(var(--a) * 120px);
                }
            }
        }

        .error-title {
            font-size: calc(var(--a) * calc(20px + (36 - 20) * ((100vw - 768px) / (1920 - 768))));
            font-weight: bold;
            color: #6e0002;
            margin-bottom: 30px;
        }

        a {
            font-size: calc(var(--a) * calc(16px + (18 - 16) * ((100vw - 768px) / (1920 - 768))));
            background-color: #910205;
            color: #ffffff;
            padding: 8px 10px;
            text-decoration: none;

            i {
                margin-#{$end}: 10px;
            }
        }
    }
</style>

<script>
import Multiselect from 'vue-multiselect'
import axios from 'axios'

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