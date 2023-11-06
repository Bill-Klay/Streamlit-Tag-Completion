<template>
  <v-row>
    <v-col cols="3"></v-col>
    <v-col cols="6">
      <v-text-field
        clearable
        label="Enter your query"
        v-model="search"
        @input="onChange"
        prepend-icon="$vuetify"
        @keydown.up.prevent="onUp"
        @keydown.down.prevent="onDown"
        @keydown.enter.prevent="onEnter"
      >
      </v-text-field>
      <v-list v-if="filteredStrings.length">
        <v-list-item
          v-for="(str, index) in filteredStrings"
          :key="index"
          @click="selectString(str)"
          :class="{'highlight': index === focusIndex}"
        >
          <v-list-item-title>{{ str }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-col>
    <v-col cols="3"></v-col>
  </v-row>
</template>


<script>
  export default {
    data() {
      return {
        strings: ['@John', '@Jane', '@Doe', '@Smith'],
        search: '',
        focusIndex: -1
      };
    },
    computed: {
      filteredStrings() {
        if (!this.search.includes('@')) {
          return [];
        }
        let searchTerm = this.search.split('@').pop();
        return this.strings.filter(str => str.toLowerCase().includes(searchTerm.toLowerCase()));
      }
    },
    methods: {
      selectString(str) {
        let parts = this.search.split('@');
        parts.pop();
        parts.push(str);
        this.search = parts.join('@');
      },
      onChange() {
        // logic to handle '@' detection
        if (this.search.includes('@')) {
          // logic to handle autocompletion
        }
      },
      onUp() {
        if (this.focusIndex > 0) {
          this.focusIndex--;
        }
      },
      onDown() {
        if (this.focusIndex < this.filteredStrings.length - 1) {
          this.focusIndex++;
        }
      },
      onEnter() {
        if (this.focusIndex >= 0 && this.focusIndex < this.filteredStrings.length) {
          this.selectString(this.filteredStrings[this.focusIndex]);
        }
      },
    }
  }
</script>

<style scoped>
.highlight {
  background-color: #f0f0f0;  /* Light gray background */
  color: #000000;  /* Black text */
}
</style>
