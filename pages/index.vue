<template>
  <section class="section">
    <div class="columns is-mobile">
      <div class="column">
        <h1 class="title">Weekly Timesheet</h1>
      </div>
    </div>
    <div class="columns">
      <div class="column is-3">
        <b-field label="Week Commencing">
          <b-datepicker
            :indicators="indicators"
            v-model="weekCommencing"
            :first-day-of-week="1"
            :show-week-number="showWeekNumber"
            placeholder="Click to select..."
            icon="calendar-today"
            trap-focus
            :unselectable-days-of-week="[0,1,2,3,5,6]"
            :nearby-selectable-month-days="true"
          ></b-datepicker>
        </b-field>
      </div>
      <div class="column is-3">
        <b-field label="Name">
          <b-input v-model="name"></b-input>
        </b-field>
      </div>
    </div>
    <div class="columns">
      <div class="column">
        <h3 class="title is-3">Days</h3>
      </div>
    </div>
    <template v-if="weekCommencing">
      <div class="columns" v-for="(day, index) in dayData" :key="day.day">
        <b-collapse
          style="width:100%"
          class="card"
          animation="slide"
          :open="day.is_open == index"
          @open="day.is_open = index"
        >
          <div slot="trigger" slot-scope="props" class="card-header" role="button">
            <p class="card-header-title">{{day.day}} - {{day.date}}</p>
            <a class="card-header-icon">
              <b-icon :icon="props.open ? 'menu-down' : 'menu-up'"></b-icon>
            </a>
          </div>
          <div class="card-content">
            <div class="content">
              <div class="columns">
                <div class="column">
                  <b-field label="Start Time">
                    <b-timepicker
                      v-model="day.shift_start"
                      placeholder="Select a time..."
                      icon="clock"
                      editable
                    ></b-timepicker>
                  </b-field>
                </div>
                <div class="column">
                  <b-field label="Finish Time">
                    <b-timepicker
                      v-model="day.shift_finish"
                      placeholder="Select a time..."
                      icon="clock"
                      editable
                    ></b-timepicker>
                  </b-field>
                </div>
                <div class="column">
                  <b-field label="Total Hours">
                    <b-timepicker
                      v-model="day.total_hours"
                      placeholder="Select a time..."
                      icon="clock"
                      editable
                    ></b-timepicker>
                  </b-field>
                </div>
                <div class="column">
                  <b-field label="20 Min Break">
                    <b-checkbox v-model="day.break_20"></b-checkbox>
                  </b-field>
                </div>

                <div class="column">
                  <b-field label="30 Min Break">
                    <b-checkbox v-model="day.break_30"></b-checkbox>
                  </b-field>
                </div>
              </div>
              <div class="columns">
                <div class="column title-col">
                  <h3 class="title is-4">Sites</h3>
                </div>
                <b-button icon-right="plus" @click="addSite(day)" />
              </div>
              <div class="columns">
                <div class="column">
                  <div class="list is-hoverable">
                    <li class="list-item" v-for="(site, index) in day.sites" :key="index">
                      <div class="columns">
                        <div class="column">
                          <b-field label="Site">
                            <b-input v-model="site.title"></b-input>
                          </b-field>
                        </div>
                        <div class="column">
                          <b-field label="Start Time">
                            <b-timepicker
                              v-model="site.start"
                              placeholder="Select a time..."
                              icon="clock"
                              editable
                            ></b-timepicker>
                          </b-field>
                        </div>
                        <div class="column">
                          <b-field label="Finish Time">
                            <b-timepicker
                              v-model="site.finish"
                              placeholder="Select a time..."
                              icon="clock"
                              editable
                            ></b-timepicker>
                          </b-field>
                        </div>
                        <div class="column">
                          <div class="buttons">
                            <b-button
                              @click="deleteSite(index,day.sites)"
                              v-if="index !== 0"
                              type="is-danger"
                              icon-right="delete"
                            />
                          </div>
                        </div>
                      </div>
                    </li>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </b-collapse>
      </div>
    </template>
  </section>
</template>

<script>
import Card from "~/components/Card";

export default {
  name: "HomePage",
  data() {
    return {
      showWeekNumber: false,
      name: "",
      weekCommencing: null,
      dayData: [
        {
          date: null,
          day: "Thursday",
          break_30: false,
          break_20: false,
          shift_start: null,
          shift_finish: null,
          total_hours: null,
          signature: false,
          is_open: 0,
          sites: [
            {
              id: 0,
              title: "",
              start: null,
              finish: null
            }
          ]
        },
                {
          date: null,
          day: "Friday",
          break_30: false,
          break_20: false,
          shift_start: null,
          shift_finish: null,
          total_hours: null,
          signature: false,
          is_open: 0,
          sites: [
            {
              id: 0,
              title: "",
              start: null,
              finish: null
            }
          ]
        },
                {
          date: null,
          day: "Saturday",
          break_30: false,
          break_20: false,
          shift_start: null,
          shift_finish: null,
          total_hours: null,
          signature: false,
          is_open: 0,
          sites: [
            {
              id: 0,
              title: "",
              start: null,
              finish: null
            }
          ]
        },
                {
          date: null,
          day: "Sunday",
          break_30: false,
          break_20: false,
          shift_start: null,
          shift_finish: null,
          total_hours: null,
          signature: false,
          is_open: 0,
          sites: [
            {
              id: 0,
              title: "",
              start: null,
              finish: null
            }
          ]
        },
                {
          date: null,
          day: "Monday",
          break_30: false,
          break_20: false,
          shift_start: null,
          shift_finish: null,
          total_hours: null,
          signature: false,
          is_open: 0,
          sites: [
            {
              id: 0,
              title: "",
              start: null,
              finish: null
            }
          ]
        },
                {
          date: null,
          day: "Tuesday",
          break_30: false,
          break_20: false,
          shift_start: null,
          shift_finish: null,
          total_hours: null,
          signature: false,
          is_open: 0,
          sites: [
            {
              id: 0,
              title: "",
              start: null,
              finish: null
            }
          ]
        },
                {
          date: null,
          day: "Wednesday",
          break_30: false,
          break_20: false,
          shift_start: null,
          shift_finish: null,
          total_hours: null,
          signature: false,
          is_open: 0,
          sites: [
            {
              id: 0,
              title: "",
              start: null,
              finish: null
            }
          ]
        },
      ]
    };
  },
  computed: {
    indicators() {
      if (!this.weekCommencing) {
        return;
      }
      _.forEach(this.dayData, (day, index) => {
        day.date = this.$moment(this.weekCommencing)
          .add(index, "days")
          .format("DD/MM/YYYY");
      });
    }
  },
  methods: {
    deleteSite(id, sites) {
      sites.splice(id, 1);
    },
    addSite(day) {
      let id = day.sites.length;
      day.sites.push({
        id: id,
        title: "",
        start: null,
        finish: null
      });
    }
  },
  components: {
    Card
  }
};
</script>
<style >
.buttons {
  justify-content: flex-end;
  height: 100%;
  align-items: flex-end;
}
.title-col {
  padding-bottom: 0;
}
.title-col h3 {
  margin-bottom: 0;
}
</style>
