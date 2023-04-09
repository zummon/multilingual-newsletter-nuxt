<template>
  <div class="uk-padding" uk-grid>
    <div class="uk-width-expand@s">
      <h3
        class="uk-margin-small"
        v-bind:style="{ fontFamily: language.fontFamily }"
      >
        {{ language["head_line"] }}
      </h3>
      <p class="uk-margin-small">
        <a
          class="uk-text-secondary"
          href="https://zummon.page/"
          target="_blank"
        >
          <u>{{ language["made_by"] }}</u>
        </a>
        {{ language["translate_by"] }}
      </p>
    </div>
    <div class="uk-width-auto@s">
      <select
        class="uk-select"
        v-bind:value="language.locale"
        v-on:change="handleLanguage($event.currentTarget.value)"
      >
        <option
          v-for="item in languages"
          v-bind:value="item.locale"
          v-bind:key="item.locale"
        >
          {{ item.name }}
        </option>
      </select>
    </div>
  </div>
  <div class="uk-grid-small uk-grid-divider" uk-grid>
    <div class="uk-width-1-3@s">
      <!-- https://pixabay.com/images/id-3025022/ -->
      <img
        class="uk-align-center uk-border-rounded"
        src="https://cdn.pixabay.com/photo/2017/12/17/21/44/coffee-3025022_960_720.jpg"
        alt="Image"
        uk-img
      />
      <p>
        {{ language["whats_it"] }}
      </p>
      <p class="uk-text-center">
        <!-- https://tablericons.com/ -->
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="48"
          height="48"
          viewBox="0 0 24 24"
          stroke-width="1"
          stroke="#9e9e9e"
          fill="none"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <path stroke="none" d="M0 0h24v24H0z" fill="none" />
          <circle cx="7" cy="7" r="1" />
          <circle cx="12" cy="12" r="1" />
          <circle cx="17" cy="17" r="1" />
        </svg>
      </p>
    </div>
    <div class="uk-width-2-3@s">
      <div class="uk-grid-small uk-child-width-1-2@s uk-grid-divider" uk-grid>
        <div>
          <p class="uk-dropcap">
            {{ language["other_text_1"] }}
          </p>
        </div>
        <div>
          <p class="uk-dropcap">
            {{ language["other_text_2"] }}
          </p>
        </div>
      </div>
      <hr />
      <p class="uk-dropcap">
        {{ language["other_text_3"] }}
      </p>
    </div>
  </div>
</template>

<script>
import languages from "./languages";

export default {
  name: "App",
  components: {},
  data() {
    return {
      languages,
      language: languages[0]
    };
  },
  methods: {
    handleLanguage(locale) {
      // find the language in languages variable
      var filtered = languages.filter(function(item) {
        return item.locale === locale;
      });

      // get the actual existing language
      if (filtered.length >= 1) {
        this.language = filtered[0];
      } else {
        this.language = languages[0];
      }
      // do stuff on this website
      document.documentElement.lang = this.language.locale;
      document.documentElement.style.fontFamily = this.language.fontFamily;
      // document.title = this.language.title

      // save to user's setting
      // localStorage.setItem("language", this.language.locale)
    }
  },
  mounted() {
    // get the user's setting
    this.handleLanguage(/* localStorage.getItem("language") */);
  }
};
</script>
