<script setup>
import IconBook from "@/components/icons/IconBook.vue";
import IconSearch from "@/components/icons/IconSearch.vue";
import IconSpeaker from "@/components/icons/IconSpeaker.vue";
import IconDocument from "@/components/icons/IconDocument.vue";
</script>

<template>
  <div
    class="flex flex-col md:flex-row md:h-screen md:overflow-hidden py-6 px-5 md:p-0"
  >
    <!-- first section of page here -->
    <section
      class="bg-white w-full md:min-h-screen md:w-1/3 md:py-8 md:px-12 md:overflow-y-scroll scrollbar-hide"
    >
      <!-- logo section here -->
      <div class="flex space-x-6 items-center mb-6 md:mb-12">
        <IconBook class="w-12 h-12 text-orange-400" />
        <h2 class="font-mono text-xl">Dictionary</h2>
      </div>
      <!-- logo section ends here -->

      <!-- Search form starts here -->
      <form class="flex flex-col items-center space-y-4 w-full mb-12">
        <div
          class="w-full h-10 rounded-full flex items-center justify-center px-1 bg-gray-100"
        >
          <input
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
      </form>
      <!-- search form ends here -->

      <!-- Word and play starts here -->
      <div class="mb-8">
        <h1 class="text-5xl font-bold mb-4">Weekend</h1>
        <h2 class="text-lg text-gray-500 font-semibold font-mono mb-3">
          [ wi:kend ]
        </h2>
        <div class="space-x-6">
          <button
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
          See synonyms for: weekend / weekended / weekending on Thesaurus.com
        </p>
        <p class="text-gray-500 text-sm">
          learn more about <span class="text-black font-bold">weekend</span> on
          <a
            href="https://en.wiktionary.org/wiki/weekend"
            class="text-orange-400"
            >Wikitionary</a
          >
        </p>
      </div>
      <!-- See more ends here -->

      <!-- buttons section starts here -->
      <div class="flex space-x-2 mb-8">
        <div
          class="text-sm px-4 py-2 rounded-full w-fit text-white bg-orange-300 cursor-pointer hover:bg-orange-400"
        >
          Definitions
        </div>
        <div
          class="text-sm px-4 py-2 rounded-full w-fit text-white bg-orange-300 cursor-pointer hover:bg-orange-400"
        >
          Examples
        </div>
        <div
          class="text-sm px-4 py-2 rounded-full w-fit text-white bg-orange-300 cursor-pointer hover:bg-orange-400"
        >
          Synonyms
        </div>
      </div>
      <!-- buttons section ends here -->
    </section>

    <!-- Second section of page here -->

    <section
      class="bg-white md:bg-gray-200 w-full md:w-2/3 md:py-8 md:px-12 md:overflow-y-scroll scrollbar-hide"
    >
      <!-- Definitions start here -->
      <div class="mb-6">
        <div>
          <h1 class="text-lg font-mono text-gray-600 font-semibold mb-4">
            Definitions
          </h1>
          <div class="w-full h-[1px] bg-gray-300 mb-2"></div>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-2 md:gap-4">
          <div
            class="bg-white md:h-[250px] rounded p-4 md:overflow-y-hidden scrollbar-hide"
          >
            <h2 class="font-semibold text-gray-600 mb-3">Noun</h2>
            <ul
              class="list-disc text-sm list-inside text-gray-500 space-y-3 md:pb-10 md:h-full md:overflow-y-scroll scrollbar-hide"
            >
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
              <li>
                The break in the working week, usually two days including the
                traditional holy or sabbath day. Thus in western countries,
                Saturday and Sunday.
              </li>
              <li>
                The break in the working week, usually two days including the
                traditional holy or sabbath day. Thus in western countries,
                Saturday and Sunday.
              </li>
            </ul>
          </div>
          <div class="bg-white md:h-[250px rounded p-4">
            <h2 class="font-semibold text-gray-600 mb-3">Verb</h2>
            <ul class="list-disc text-sm list-inside text-gray-500 space-y-2">
              <li>
                The break in the working week, usually two days including the
                traditional holy or sabbath day. Thus in western countries,
                Saturday and Sunday.
              </li>
            </ul>
          </div>
        </div>
      </div>
      <!-- definitions ends here -->

      <!-- Examples start here -->
      <div class="mb-6">
        <div>
          <h1 class="text-lg font-mono text-gray-600 font-semibold mb-4">
            Examples & Synonyms
          </h1>
          <div class="w-full h-[1px] bg-gray-300 mb-2"></div>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-2 md:gap-4">
          <div class="bg-white md:h-[250px] rounded p-4">
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
          <div class="bg-white md:h-[250px rounded p-4">
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
      </div>
      <!-- examples ends here -->
    </section>
  </div>
</template>
