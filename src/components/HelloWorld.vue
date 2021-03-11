<template>
  <div class="hello">
    <div>
      <b-input-group>
        <b-form-input type="search" v-model="filterObj.text"></b-form-input>
        <b-input-group-append is-text>
          <span style="width: 1rem;">
            <b-spinner small v-if="filtering"></b-spinner>
            <span v-else>&nbsp;</span>
          </span>
        </b-input-group-append>
      </b-input-group>
      <b-table show-empty
               sticky-header="1250px"
               no-border-collapse
               :items="items"
               :fields="['name', 'number']"
               :filter="filterObj"
               :filter-function="filterFunction"
               small
               hover
               @filtered="onFiltered"
      >
      </b-table>
      <p>
        Filter: {{ this.filterObj.text }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      items: (new Array(200)).fill('').map((v, index) => (
          { name: `Item ${index}`, number: index }
      )),
      filterObj: {text:''},
      filtering: false
    }
  },
  computed: {
    computedfilter() {
      return this.filterText ? this.filterText : '';
    },
  },
  watch: {
    "filterObj.text"( ) {
      this.filtering = true
    }
  },
  methods: {
    onFiltered() {
      this.filtering = false
    },
    filterFunction(item, criteria) {
      console.log('run')
      return item.name.includes(criteria.text);

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
