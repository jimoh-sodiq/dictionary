<script setup>
import IconBook from "@/components/icons/IconBook.vue";
import IconSearch from "@/components/icons/IconSearch.vue";
import IconSpeaker from "@/components/icons/IconSpeaker.vue";
import IconDocument from "@/components/icons/IconDocument.vue";
import { ref, computed, watchEffect, onMounted, watch } from "vue";

const searchText = ref("");
const searchResult = ref([]);
const suggestions = ref([]);
const SEARCH_WORD_URL = computed(() => {
  return `https://api.dictionaryapi.dev/api/v2/entries/en/${searchText.value}`;
});
const userHasSearched = ref(false);
const toggleSuggestion = ref(false);

onMounted(() => {
  generateAndDisplayMeaning();
});
async function generateAndDisplayMeaning() {
  const randomWord = await (
    await fetch("https://random-words-api.vercel.app/word")
  ).json();
  searchResult.value = randomWord;
}

async function searchWord() {
  try {
    searchResult.value = await (await fetch(SEARCH_WORD_URL.value)).json();
    userHasSearched.value = true;
    toggleSuggestion.value = false;
    console.log(searchResult.value);
  } catch {
    (err) => {
      console.log("error is:" + err);
    };
  }
}

function displaySuggestion(word) {
  searchText.value = word;
  toggleSuggestion.value = false;
}

function playSound() {
  for (let i = 0; i <= searchResult.value[0].phonetics.length; i++) {
    if (searchResult.value[0].phonetics[i].audio) {
      const audio = new Audio(searchResult.value[0].phonetics[i].audio);
      audio.play();
      break;
    } else {
      continue;
    }
  }
}

watchEffect(async () => {
  const url = `https://api.datamuse.com/sug?s=${searchText.value}`;
  suggestions.value = await (await fetch(url)).json();
});

watch(
  () => searchText.value,
  () => {
    toggleSuggestion.value = true;
  }
);
</script>

<template>
  <div
    class="flex flex-col md:flex-row md:h-screen md:overflow-hidden py-6 px-5 md:p-0"
  >
    <!-- first section of page here -->
    <section
      @click.self="toggleSuggestion = false"
      class="bg-white w-full md:min-h-screen md:w-1/3 md:py-8 md:px-12 md:overflow-y-scroll scrollbar-hide mb-12 md:mb-0"
    >
      <!-- logo section here -->
      <div class="flex space-x-6 items-center mb-6 md:mb-12">
        <IconBook class="w-12 h-12 text-orange-400" />
        <h2 class="font-mono text-xl">Dictionary</h2>
      </div>
      <!-- logo section ends here -->

      <!-- Search form starts here -->
      <form
        class="flex flex-col items-center space-y-4 w-full mb-12 relative"
        @submit.prevent="searchWord"
      >
        <div
          class="w-full h-10 rounded-full flex items-center justify-center px-1 bg-gray-100"
        >
          <input
            v-model="searchText"
            required
            type="text"
            inputmode="text"
            placeholder="Search Words"
            class="h-full outline-none text-xl font-mono text-gray-700 bg-gray-100 flex-1 rounded-full px-3 w-full place"
          />
          <button
            type="submit"
            class="bg-white flex items-center cursor-pointer justify-center h-9 w-9 rounded-full group"
          >
            <IconSearch
              class="text-orange-500 w-4 hover:w-7 transition-all group-hover:w-7"
            />
          </button>
        </div>

        <div
          v-show="
            searchText && suggestions.length > 0 && toggleSuggestion === true
          "
          class="bg-gray-100 w-full text-left p-3 absolute top-10 rounded"
        >
          <div
            v-for="(suggestion, index) in suggestions.slice(0, 6)"
            :key="index"
            class="w-full text-gray-600 cursor-pointer p-1"
            @click="displaySuggestion(suggestion.word)"
          >
            <hr v-if="index > 0" />
            {{ suggestion.word }}
          </div>
        </div>
      </form>

      <!-- search form ends here -->
      <div v-if="userHasSearched === false && searchResult" class="mb-8">
        <p class="font-semibold text-gray-600 mb-4">New Word for you:</p>
        <h1 class="text-5xl font-bold mb-4 text-center md:text-left">
          {{ searchResult[0]?.word }}
        </h1>
        <span class="text-sm text-orange-500 font-semibold mb-3">Meaning:</span>
        <p class="text-lg text-gray-700 font-semibold mb-3">
          {{ searchResult[0]?.definition }}
        </p>
        <span class="text-sm text-orange-500 font-semibold mb-3"
          >Pronunciation:</span
        >
        <p class="text-lg text-gray-700 font-semibold">
          {{ searchResult[0]?.pronunciation }}
        </p>
      </div>

      <div v-else-if="searchResult && userHasSearched === true">
        <!-- Word and play starts here -->
        <div class="mb-8">
          <h1 class="text-5xl font-bold mb-4">
            {{ searchResult[0]?.word }}
          </h1>
          <h2 class="text-lg text-gray-500 font-semibold font-mono mb-3">
            [ {{ searchResult[0]?.phonetic }} ]
          </h2>
          <div class="space-x-6">
            <button
              @click="playSound"
              class="cursor-pointer bg-orange-100 text-center p-2 rounded w-14 h-14 hover:bg-orange-200 transition-all"
            >
              <IconSpeaker class="text-orange-400 w-6 mx-auto" />
              <span class="text-sm font-semibold text-orange-300">Play</span>
            </button>
            <button
              class="cursor-pointer bg-orange-100 text-center p-2 rounded w-14 h-14 hover:bg-orange-200 transition-all"
            >
              <IconDocument class="text-orange-400 w-6 mx-auto" />
              <span class="text-sm font-semibold text-orange-300">Copy</span>
            </button>
          </div>
        </div>
        <!-- Word and play ends here -->

        <!-- See more starts here -->
        <div class="space-y-3 mb-6">
          <p class="text-sm text-gray-500">
            See the licence for {{ searchResult[0].word }}
            <a
              target="_blank"
              :href="searchResult[0].license.url"
              class="text-orange-400"
              >here</a
            >
          </p>
          <p class="text-gray-500 text-sm">
            learn more about
            <span class="text-black font-bold">{{ searchResult[0].word }}</span>
            on
            <a
              target="_blank"
              :href="searchResult[0].sourceUrls"
              class="text-orange-400"
              >Wikitionary</a
            >
          </p>
        </div>
        <!-- See more ends here -->

        <!-- buttons section starts here -->
        <div class="flex space-x-2 mb-8">
          <a
            href="#"
            class="text-sm px-4 py-2 rounded-full w-fit text-white bg-orange-300 cursor-pointer hover:bg-orange-400"
          >
            Definitions
          </a>
          <a
            
            class="text-sm px-4 py-2 rounded-full w-fit text-white bg-orange-300 cursor-pointer hover:bg-orange-400"
          >
            Examples
          </a>
          <a
            
            class="text-sm px-4 py-2 rounded-full w-fit text-white bg-orange-300 cursor-pointer hover:bg-orange-400"
          >
            Synonyms
          </a>
        </div>
        <!-- buttons section ends here -->
      </div>
    </section>

    <!-- Second section of page here -->

    <section
      @click.self="toggleSuggestion = false"
      class="bg-white md:bg-gray-100 w-full md:w-2/3 md:py-8 md:px-12 md:overflow-y-scroll scrollbar-hide"
    >
      <!-- Definitions start here -->
      <div
        v-if="userHasSearched === false"
        class="flex flex-col items-center justify-center w-full h-full text-center text-xl md:text-2xl text-gray-500 font-semibold font-mono"
      >
        <h1 class="text-orange-500">Need information about a word?</h1>
        <h2>
          Just type in the word in the search input and click on the search icon
        </h2>
      </div>
      <div v-else>
        <div class="mb-6">
          <div id="definitions">
            <h1 class="text-lg font-mono text-gray-600 font-semibold mb-4">
              Definitions
            </h1>
            <div class="w-full h-[1px] bg-gray-300 mb-2"></div>
          </div>
          <div class="w-full">
            <!-- grid grid-cols-1 md:grid-cols-2 gap-2 md:gap-4 -->
            <div v-for="(item, index) in searchResult" :key="index">
              <!-- {{ item }} -->
              <div
                class="p-4"
                v-for="(unique, index) in item.meanings"
                :key="index"
              >
                <h2 class="font-semibold text-gray-800 text-xl uppercase">
                  {{ unique.partOfSpeech }}
                </h2>
                <ul
                  v-for="(definition, index) in unique.definitions"
                  :key="index"
                  class="list-disc text-sm list-inside text-gray-600"
                >
                  <li class="mb-2">
                    {{ definition.definition }}
                    <br />
                    <p class="text-xs pl-6" v-if="definition.example">
                      <span class="font-bold text-gray-800">Example:</span>
                      {{ definition.example }}
                    </p>
                    <br />
                    <p
                      class="text-xs pl-6"
                      v-if="definition.synonyms.length > 0"
                    >
                      <span class="font-bold text-gray-800">Synonyms:</span>
                      <span
                        v-for="(syn, index) in definiton.synonyms"
                        :key="index"
                        >{{ syn }},</span
                      >
                    </p>
                    <p
                      class="text-xs pl-6"
                      v-if="definition.antonyms.length > 0"
                    >
                      <span class="font-bold text-gray-800">Antonyms:</span>
                      <span
                        v-for="(ant, index) in definiton.antonyms"
                        :key="index"
                        >{{ ant }},</span
                      >
                    </p>
                  </li>
                </ul>
              </div>
            </div>
            <!-- <div class="bg-white md:h-[250px rounded p-4">
              <h2 class="font-semibold text-gray-600 mb-3">Verb</h2>
              <ul class="list-disc text-sm list-inside text-gray-500 space-y-2">
                <li>
                  The break in the working week, usually two days including the
                  traditional holy or sabbath day. Thus in western countries,
                  Saturday and Sunday.
                </li>
              </ul>
            </div> -->
          </div>
        </div>
        <!-- definitions ends here -->

        <!-- Examples start here
        <div class="mb-6">
          <div>
            <h1 class="text-lg font-mono text-gray-600 font-semibold mb-4">
              Examples & Synonyms
            </h1>
            <div class="w-full h-[1px] bg-gray-300 mb-2"></div>
          </div>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-2 md:gap-4">
            <div class="bg-white md:h-[250px] rounded p-4" id="examples">
              <h2 class="font-semibold text-gray-600 mb-3">Examples</h2>
              <ul class="list-disc text-sm list-inside text-gray-500 space-y-3">
                <li>
                  The break in the working week, usually two days including the
                  traditional holy or sabbath day. Thus in western countries,
                  Saturday and Sunday.
                  <span
                    class="bg-orange-400 cursor-pointer text-orange-100 text-xs px-4 hover:bg-orange-300 transition-all py-1 rounded-full"
                    >Copy</span
                  >
                </li>
                <li>
                  The break in the working week, usually two days including the
                  traditional holy or sabbath day. Thus in western countries,
                  Saturday and Sunday.
                </li>
              </ul>
            </div>
            <div class="bg-white md:h-[250px rounded p-4" id="synonyms">
              <h2 class="font-semibold text-gray-600 mb-3">Synonyms</h2>
              <ul class="list-disc text-sm list-inside text-gray-500 space-y-2">
                <li>
                  The break in the working week, usually two days including the
                  traditional holy or sabbath day. Thus in western countries,
                  Saturday and Sunday.
                </li>
              </ul>
            </div>
          </div>
        </div> -->
      </div>
      <!-- examples ends here -->
    </section>
  </div>
</template>
