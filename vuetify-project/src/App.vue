<template>
  <v-row no-gutters>
    <v-col cols="3"></v-col>
    <v-col cols="6">
      <div class="suggestion position-absolute ma-4">{{ suggestion.slice(search.length - searchTerm.length) }}</div>
      <v-text-field
        label="Type here..."
        v-model="search"
        @input="onChange"
        @keydown.tab.prevent="onTab"
        class="position-relative ma-8"
      ></v-text-field>
    </v-col>
    <v-col cols="3"></v-col>
  </v-row>
</template>

<script>
  export default {
    data() {
      return {
        strings: ['','John', 'Jane', 'Doe', 'Smith'],
        search: '',
        suggestion: '',
        searchTerm: ''
      };
    },
    computed: {
      filteredStrings() {
        if (!this.search) {
          return [];
        }
        let words = this.search.split(' ');
        this.searchTerm = words[words.length - 1];
        return this.strings.filter(str => str.toLowerCase().startsWith(this.searchTerm.toLowerCase()));
      }
    },
    methods: {
      onChange() {
        let words = this.search.split(' ');

        if (this.filteredStrings.length > 0) {
          words[words.length - 1] = this.filteredStrings[0];
          this.suggestion = words.join(' ');
        } else {
          this.suggestion = '';
        }
      },
      onTab() {
        this.search = this.suggestion;
        this.suggestion = '';
      },
    }
  }
</script>

<style scoped>
  .suggestion {
    color: lightgreen;
    line-height: 0px; /* Adjust this to match the height of your text field */
    left: 27%; /* Adjust this to match the left padding of your text field */
    pointer-events: none; /* This prevents the suggestion div from blocking interactions with the text field */
  }
</style>
