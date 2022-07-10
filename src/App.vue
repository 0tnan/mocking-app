<template>
  <div id="app" class="App">
    <h1 class="App-title">
      The Mocking&nbsp;<span class="App-title App-title--colored">App</span>
    </h1>
    <div class="App-content">
      <p class="App-text">Enter Your Text Here :</p>
      <textarea class="App-textEntry" v-model="entry"></textarea>
      <p class="App-text">Your Dumb Text Output :</p>
      <button
        @click="changeColor()"
        :class="{ 'App-copyButton--clicked': switchColor }"
        class="App-copyButton"
        type="button"
        v-clipboard:copy="result"
        v-click-outside="removeColor"
      >
        <CopyLogo class="App-logo App-logo--alt" />
      </button>
      <div class="App-textResults">{{ result }}</div>
    </div>
    <footer class="App-footer">
      <div class="App-footerIcons">
        <a href="https://github.com/Andriamanantoanina" target="blank">
          <GithubLogo class="App-logo" />
        </a>
        <a href="https://rakotondranaly.fr" target="blank">
          <WebsiteLogo class="App-logo" />
        </a>
      </div>
      <p>Copyright 2022 - Nanto</p>
    </footer>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import GithubLogo from "@/assets/icons/github.svg";
import WebsiteLogo from "@/assets/icons/globe.svg";
import CopyLogo from "@/assets/icons/copy.svg";
import ClickOutside from "vue-click-outside";

export default Vue.extend({
  components: {
    GithubLogo,
    WebsiteLogo,
    CopyLogo,
  },
  data() {
    return {
      entry: "",
      switchColor: false,
    };
  },
  directives: {
    ClickOutside,
  },
  computed: {
    result(): string {
      return this.transformText(this.entry);
    },
  },
  methods: {
    transformText(input: string): string {
      let output = input;
      [...input].forEach((char, index) => {
        if (index % 2 !== 0) {
          output = this.replaceAt(output, index, char.toUpperCase());
        }
      });
      return output;
    },
    replaceAt(input: string, index: number, replacement: string): string {
      return (
        input.substring(0, index) +
        replacement +
        input.substring(index + replacement.length)
      );
    },
    changeColor(): void {
      this.switchColor = true;
    },
    removeColor(): void {
      this.switchColor = false;
    },
  },
});
</script>

<style lang="scss">
@import "src/assets/styles/main.scss";

.App {
  display: flex;
  flex-direction: column;
  justify-content: center;
  background-color: $color-primary;
  height: 100%;
  width: 100%;
  font-size: $xxl;
  font-weight: 400;

  &-title {
    margin: 5rem auto;
    font-weight: 700;

    &--colored {
      color: $color-secondary;
    }
  }

  &-logo {
    color: $white;
    fill: $white;
    transform: scale(2);

    &--alt {
      transform: scale(1);
    }
  }

  &-content {
    position: relative;
    flex-grow: 1;
    display: flex;
    align-items: center;
    flex-direction: column;
    padding: 1rem 2.5rem;
  }

  &-img {
    height: 25%;
    width: 25rem;
  }

  &-copyButton {
    position: absolute;
    border-radius: 0.5rem;
    top: 33rem;
    right: 4rem;
    background: none;
    border: 0.1rem solid $color-secondary;
    height: 4rem;
    width: 4rem;
    transition: all ease-in-out 0.5s;

    &--clicked {
      background: $white;

      svg {
        fill: $color-primary;
      }
    }
  }

  &-footer {
    display: flex;
    flex-direction: column;
    padding: 0 8rem;
    height: 12rem;
    justify-content: center;
    font-size: $s;
    font-style: italic;

    &Icons {
      display: flex;
      justify-content: space-evenly;
    }

    p {
      margin-top: 2.5rem;
      text-align: center;
    }
  }

  &-text {
    font-size: $l;
    align-self: flex-start;
    padding-left: 4rem;

    &Entry {
      margin: 2.5rem 0;
      padding: 0;
      max-height: 25rem;
      height: 25rem;
      width: calc(100% - 9rem);
      overflow: auto;
      resize: none;
      -moz-border-bottom-colors: none;
      -moz-border-left-colors: none;
      -moz-border-right-colors: none;
      -moz-border-top-colors: none;
      background: none repeat scroll 0 0 $color-primary;
      border-color: -moz-use-text-color $color-secondary $color-secondary -moz-use-text-color;
      border-image: none;
      border-radius: 0.6rem 0.6rem 0.6rem 0.6rem;
      border-style: none solid solid none;
      border-width: medium 0.1rem 0.1rem medium;
      box-shadow: 0 0.1rem 0.2rem $color-secondary inset;
      color: $color-primary;
      font-family: $font-primary;
      font-size: $l;
      line-height: 1.4em;
      padding: 0.5rem 0.8rem;
      transition: background-color 0.5s ease-in-out 0s;

      &:focus {
        background: none repeat scroll 0 0 $white;
        outline-width: 0;
      }
    }

    &Results {
      max-height: 20rem;
      width: calc(100% - 9rem);
      word-wrap: break-word;
      flex-grow: 1;
      margin-top: 2.5rem;
      font-size: $l;
      align-self: flex-start;
      padding-left: 4rem;
      color: $color-secondary;
      line-height: 1.4em;
      overflow: auto;
    }
  }
}
</style>
