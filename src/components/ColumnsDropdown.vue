<template>
    <div class="dropdown">
        <button class="btn btn-secondary dropdown-toggle" type="button"
                @click="dropdown = !dropdown" aria-haspopup="true"
                aria-expanded="false">
            {{columns}}
        </button>
        <div class="dropdown-menu" aria-labelledby="dropdownMenuButton"
             v-bind:class="{ show: dropdown }">
            <a class="dropdown-item"
               @click="selectColumns(1)">1</a>
            <a class="dropdown-item"
               @click="selectColumns(2)">2</a>
            <a class="dropdown-item"
               @click="selectColumns(3)">3</a>
        </div>
    </div>
</template>

<script>
  import {createNotification} from './../js/notification';
  export default {
    props: [],
    data () {
      return {
        dropdown: false,
        columns: 2
      };
    },
    computed: {
    },
    methods: {
      selectColumns: function (columns) {
        this.dropdown = !this.dropdown;
        this.columns = columns;
        this.saveColumns();
      },
      reset: function () {
        this.fps = 1;
        this.dropdown = !this.dropdown;
      },
      saveColumns: function () {
        localStorage.setItem('columns', this.columns);
        createNotification("Settings Saved");
      }
    },
    created: function () {
      const columns = localStorage.getItem('columns');
      if(columns) {
        this.columns = columns
      } else {
        this.saveColumns();
      }
    }
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .show {
        display: block;
    }

    .hidden {
        display: none;
    }
</style>
