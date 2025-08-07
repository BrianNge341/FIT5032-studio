<!-- JSONLab.vue -->
<template>
  <div class="json-lab">
    <h1>🗄️ JSON Data & Vue Directives Lab</h1>

    <section class="lab-section">
      <h2>📚 Working with JSON Arrays</h2>
      <p>Our <code>authors.json</code> contains an array of author objects.</p>

      <h3>Iterating through Arrays</h3>
      <!-- Activity 6: Render a list containing author names and their birth years. Hint: Make use of the v-for directive to iterate through the array of authors. -->
      <!-- TODO: CODE TO RENDER LIST OF AUTHORS HERE -->
      <ul>
        <li v-for="author in authors" :key="author.id">
          {{ author.name }} ({{ author.birthYear }})
        </li>
      </ul>
      
      <h3>Filtering Arrays</h3>
      <!-- Activity 7: Render a list containing authors born after 1850. Hint: Make use of the v-for directive to iterate through the array of authors that you have filtered out. -->
      <p>Authors born after 1850:</p>
      <!-- TODO: CODE TO RENDER LIST OF AUTHORS HERE -->
      <ul>
        <li v-for="author in modernAuthors" :key="author.id">
          {{ author.name }} ({{ author.birthYear }})
        </li>
      </ul>

      <h3>Mapping Arrays</h3>
      <p>Famous works:</p>
      <ul>
        <!-- Activity 8: Render a list of all famous works. Hint: Use the v-for directive to iterate through the array of authors that you have filtered out. -->
        <!-- TODO: CODE TO RENDER LIST OF FAMOUS WORKS HERE -->
        <li v-for="work in allFamousWorks" :key="work.id">
          {{ work }}
        </li>
      </ul>

      <h3>Finding in Arrays</h3>
      <p>Finding by property: {{ orwell?.name }}</p>

      <h3>Nested Arrays/Objects</h3>
      <p>{{ austen?.name }}'s works:</p>
      <!-- Activity 9: Render a list of Austen's works. Hint: Use the v-for directive to iterate through the array of authors that you have filtered out. -->
      <!-- TODO: CODE TO RENDER LIST OF AUSTEN'S WORKS HERE -->
      <ul>
        <li v-for="work in austen?.famousWorks" :key="work.id">
          {{ work.title }} ({{ work.year }})
        </li>
      </ul>
    </section>

    <section class="lab-section">
      <h2>🏢 Working with JSON Objects</h2>
      <p>Our <code>bookstores.json</code> is a JSON object.</p>

      <h3>Accessing Properties</h3>
      <p>
        Company:
        <!-- Activity 9a: Get the company name from the bookstores object. -->
        <!-- TODO: CODE TO GET COMPANY NAME HERE -->
        {{ bookstores.company }}
      </p>

      <p>
        Total Stores:
        <!-- Activity 9b: Get the total number of stores from the bookstores object. -->
        <!-- TODO: CODE TO GET TOTAL STORES HERE -->
        {{ bookstores.totalStores }}
      </p>

      <h3>Iterating Object Properties</h3>
      <p>Store Types:</p>
      <!-- Activity 10: Iterate through the storeTypes array and display the store type and the number of stores that use that type. -->
      <!-- TODO: CODE TO RENDER LIST OF STORE TYPES HERE -->
      <ul>
        <li v-for="(count, type) in bookstores.storeTypes" :key="type">
          {{ type }}: {{ count }} stores
        </li>
      </ul>

      <h3>Nested Objects</h3>
      <p>Opening Hours:</p>
      <!-- Activity 11: Iterate through the openingHours object and display the day of the week and the opening and closing times. -->
      <!-- TODO: CODE TO RENDER LIST OF OPENING HOURS HERE -->
      <ul>
        <li v-for="(hours, day) in bookstores.openingHours" :key="day">
          {{ day }}: {{ hours.open }} - {{ hours.close }}
        </li>
      </ul>

      <h3>Working with Arrays in Objects</h3>
      <!-- Activity 12: Get the top sellers from the bookstores object. -->
      <!-- TODO: CODE TO GET TOP SELLERS HERE -->
      <p>We operate in:</p>
      <p>Our #1 seller:</p>
      <ul>
        <li v-for="book in bookstores.topSellers" :key="book.id">
          {{ book }}
        </li>
      </ul>
    </section>

    <section class="lab-section">
      <h2>v-if & v-else</h2>
      <p>Toggle visibility based on a condition.</p>
      <!-- Activity 13: Toggle the message visibility when the button is clicked. -->
      <!-- TODO: CODE TO TOGGLE MESSAGE VISIBILITY HERE. Hint: Use the v-if directive. -->
      <button @click="showMessage = !showMessage">Toggle Message</button>
      <p v-if="showMessage" class="message success">✨ You're a Vue superstar! ✨</p>
      <p v-else class="message">Click the button to see a message.</p>
    </section>

    <section class="lab-section">
      <h2>Attribute, Class and Style Binding with <code>v-bind</code></h2>
      <p>Highlighting Specific Authors:</p>

      <!-- Activity 14: Class Binding with Objects -->
      <h3>Class Binding with Objects</h3>
      <p>Click on authors to highlight them:</p>
      <ul>
        <li v-for="author in authors" 
            :key="author.id"
            :class="{ highlight: highlightedAuthors.includes(author.id), 'author-item': true }"
            @click="toggleHighlight(author.id)"
            style="cursor: pointer;">
          {{ author.name }} ({{ author.birthYear }})
          <span v-if="highlightedAuthors.includes(author.id)"> ⭐</span>
        </li>
      </ul>

      <!-- Activity 15: Style Binding with Objects -->
      <h3>Style Binding with Objects</h3>
      <p>Authors with dynamic styling:</p>
      <ul>
        <li v-for="author in authors" 
            :key="author.id"
            :style="{ 
              backgroundColor: getAuthorColor(author.birthYear),
              color: author.birthYear < 1850 ? '#ffffff' : '#333333',
              fontWeight: highlightedAuthors.includes(author.id) ? 'bold' : 'normal',
              border: highlightedAuthors.includes(author.id) ? '2px solid #42b883' : '1px solid #ddd'
            }"
            @click="toggleHighlight(author.id)"
            style="cursor: pointer; transition: all 0.3s ease;">
          {{ author.name }} - Born {{ author.birthYear }}
        </li>
      </ul>

      <!-- Activity 16: Class Binding with Arrays -->
      <h3>Class Binding with Arrays</h3>
      <p>Authors with multiple conditional classes:</p>
      <ul>
        <li v-for="author in authors" 
            :key="author.id"
            :class="[
              'author-card', 
              highlightedAuthors.includes(author.id) ? 'selected' : '', 
              author.birthYear > 1850 ? 'modern-author' : 'classic-author',
              { 'favorite': favoriteAuthors.includes(author.id) }
            ]"
            @click="toggleHighlight(author.id)"
            @dblclick="toggleFavorite(author.id)">
          <strong>{{ author.name }}</strong><br>
          <small>{{ author.genres.join(', ') }}</small>
          <div class="action-hints">
            <span v-if="!highlightedAuthors.includes(author.id)">Click to highlight</span>
            <span v-else>Click to unhighlight</span>
            | Double-click to {{ favoriteAuthors.includes(author.id) ? 'unfavorite' : 'favorite' }}
          </div>
        </li>
      </ul>

      <!-- Activity 17: Dynamic Attribute Binding -->
      <h3>Dynamic Attribute Binding</h3>
      <p>Authors with dynamic attributes:</p>
      <div class="author-grid">
        <div v-for="author in authors" 
             :key="author.id"
             :title="`${author.name} - Born ${author.birthYear}, Genres: ${author.genres.join(', ')}`"
             :data-author-id="author.id"
             :aria-label="`Author ${author.name}`"
             :tabindex="highlightedAuthors.includes(author.id) ? '0' : '-1'"
             class="author-badge"
             @click="toggleHighlight(author.id)">
          {{ author.name }}
        </div>
      </div>

      <!-- Control Panel -->
      <div class="control-panel">
        <h4>Controls:</h4>
        <button @click="clearHighlights" class="btn btn-secondary">Clear All Highlights</button>
        <button @click="highlightAll" class="btn btn-primary">Highlight All</button>
        <button @click="clearFavorites" class="btn btn-secondary">Clear Favorites</button>
        <p><small>Highlighted: {{ highlightedAuthors.length }} | Favorites: {{ favoriteAuthors.length }}</small></p>
      </div>

    </section>
  </div>
</template>

<script setup>
import { ref, computed } from "vue"

// Activity 1: Import JSON files (authors.json and bookstores.json)
// TODO: CODE TO IMPORT JSON FILES HERE
import authors from "../assets/json/authors.json"
import bookstores from "../assets/json/bookstores.json" 

const showMessage = ref(false)
const highlightedAuthors = ref([])
const favoriteAuthors = ref([])

// Activity 2: Get authors born after 1850
const modernAuthors = computed(() => {
  // TODO: CODE TO FILTER ARRAY OF AUTHORS HERE
  return authors.filter(author => author.birthYear > 1850)
})

// Activity 3: Get all famous works
const allFamousWorks = computed(() => {
  // TODO: CODE TO GET ALL FAMOUS WORKS HERE
  return authors.flatMap((author) => author.famousWorks.map((work) => work.title))
})

// Activity 4: Find author by name
const orwell = computed(() => {
  // TODO: CODE TO FIND AUTHOR BY NAME HERE
  return authors.find(author => author.name === "George Orwell")
})

// Activity 5: Find author by ID
const austen = computed(() => {
  // TODO: CODE TO FIND AUTHOR BY ID HERE
  return authors.find(author => author.id === 1)
})

// Methods for highlighting functionality
const toggleHighlight = (authorId) => {
  const index = highlightedAuthors.value.indexOf(authorId)
  if (index > -1) {
    highlightedAuthors.value.splice(index, 1)
  } else {
    highlightedAuthors.value.push(authorId)
  }
}

const toggleFavorite = (authorId) => {
  const index = favoriteAuthors.value.indexOf(authorId)
  if (index > -1) {
    favoriteAuthors.value.splice(index, 1)
  } else {
    favoriteAuthors.value.push(authorId)
  }
}

const clearHighlights = () => {
  highlightedAuthors.value = []
}

const highlightAll = () => {
  highlightedAuthors.value = authors.map(author => author.id)
}

const clearFavorites = () => {
  favoriteAuthors.value = []
}

const getAuthorColor = (birthYear) => {
  if (birthYear < 1800) return '#8e44ad'      // Purple for very old
  if (birthYear < 1850) return '#3498db'      // Blue for old
  if (birthYear < 1900) return '#e67e22'      // Orange for medium
  return '#27ae60'                            // Green for modern
}
</script>

<style scoped>
.json-lab {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  max-width: 80vw;
  margin: 0 auto;
  padding: 20px;
  background-color: #f4f4f4;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

h1,
h2 {
  color: #333;
}
h1 {
  text-align: center;
}

.lab-section {
  background-color: white;
  padding: 20px;
  margin-bottom: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.message {
  padding: 10px;
  border-radius: 5px;
  margin-top: 10px;
}

.success {
  background-color: #e7faf3;
  color: #42b883;
  border: 1px solid #42b883;
}

.highlight {
  background-color: #42b883;
}

code {
  background-color: #e0e0e0;
  padding: 2px 5px;
  border-radius: 4px;
  font-family: "Courier New", Courier, monospace;
}

ul {
  list-style-type: none;
  padding: 0;
}
li {
  background-color: #f0f0f0;
  padding: 10px;
  margin: 5px 0;
  border-radius: 5px;
}

/* Highlighting and binding styles */
.highlight {
  background-color: #42b883 !important;
  color: white;
  transform: scale(1.02);
  box-shadow: 0 4px 8px rgba(66, 184, 131, 0.3);
}

.author-item {
  transition: all 0.3s ease;
}

.author-item:hover {
  background-color: #e0e0e0;
  transform: translateX(5px);
}

.author-card {
  background-color: #f8f9fa;
  border: 2px solid #dee2e6;
  border-radius: 8px;
  padding: 15px;
  margin: 10px 0;
  cursor: pointer;
  transition: all 0.3s ease;
}

.author-card:hover {
  border-color: #42b883;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.selected {
  background-color: #e7faf3;
  border-color: #42b883;
  box-shadow: 0 4px 12px rgba(66, 184, 131, 0.2);
}

.modern-author {
  border-left: 4px solid #17a2b8;
}

.classic-author {
  border-left: 4px solid #6f42c1;
}

.favorite {
  background-color: #fff3cd;
  border-color: #ffc107;
}

.favorite::after {
  content: " ❤️";
}

.action-hints {
  font-size: 0.8em;
  color: #6c757d;
  margin-top: 5px;
}

.author-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin: 15px 0;
}

.author-badge {
  background-color: #e9ecef;
  padding: 8px 12px;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
  border: 1px solid #ced4da;
}

.author-badge:hover {
  background-color: #42b883;
  color: white;
  transform: translateY(-2px);
}

.author-badge[tabindex="0"] {
  background-color: #42b883;
  color: white;
  box-shadow: 0 2px 6px rgba(66, 184, 131, 0.4);
}

.control-panel {
  background-color: #f8f9fa;
  padding: 15px;
  border-radius: 8px;
  margin-top: 20px;
  border: 1px solid #dee2e6;
}

.btn {
  padding: 8px 16px;
  margin: 5px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.3s ease;
}

.btn-primary {
  background-color: #42b883;
  color: white;
}

.btn-primary:hover {
  background-color: #369870;
}

.btn-secondary {
  background-color: #6c757d;
  color: white;
}

.btn-secondary:hover {
  background-color: #545b62;
}
</style>
