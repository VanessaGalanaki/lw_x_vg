<template>
  <div v-if="showModal" class="popup">
    <div class="popup-inner">
      <button @click="showModal = false" class="popup-close">
        <font-awesome-icon icon="fa-solid fa-xmark" />
      </button>
      <p>{{ memo }}</p>
      <p>{{ author }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Popup_element",
  data() {
    return {
      showModal: false,
      memo: this.memo,
      author: this.author,
      allTriggers: [],
      type: "",
      occurance: 0,
    };
  },
  created() {
    this.quotes = [
      {
        memo: "The only true wisdom is in knowing you know nothing.",
        author: "Socrates",
      },
      {
        memo: "Tell me and I forget, teach me and I may remember, involve me and I learn.",
        author: "Benjamin Franklin",
      },
      {
        memo: "To attain knowledge, add things everyday. To attain wisdom, remove things every day.",
        author: "Lao Tse",
      },
    ];
  },
  methods: {
    popupTimerShow(time) {
      setTimeout(this.fetchRandomQuote, time);
    },
    popupScrollShow() {
      if (this.getScrollPercent() >= this.occurance) {
        window.removeEventListener("scroll", this.popupScrollShow);
        this.fetchRandomQuote();
      }
    },
    popupexitIntentShow() {
      this.fetchRandomQuote();
      document
        .getElementById("app-body")
        .removeEventListener("mouseleave", this.popupexitIntentShow);
    },
    activatePopupEngines(trg, occ) {
      this.allTriggers.push(trg.type);
      this.type = trg.type;
      this.occurance = occ;
      switch (this.type) {
        case "scroll":
          document.getElementById("app-body").classList.add("extra-body");
          window.addEventListener("scroll", this.popupScrollShow);
          break;
        case "timer":
          this.popupTimerShow(occ);
          break;
        case "exit":
          document
            .getElementById("app-body")
            .addEventListener("mouseleave", this.popupexitIntentShow);

          break;
        default:
          console.log("Hmmm no type is selected!");
      }
      //this.removeFromArray(type);
    },
    fetchRandomQuote() {
      var randomQuoteIndex = Math.floor(Math.random() * 3);     
      this.memo = this.quotes[randomQuoteIndex].memo;
      this.author = this.quotes[randomQuoteIndex].author;
      this.showModal = true;
      this.removeFromArray(this.type);
    },
    removeFromArray() {
      for (var i = 0; i < this.allTriggers.length; i++) {
        if (this.allTriggers[i] === this.type) {
          this.allTriggers.splice(i, 1);
          break;
        }
      }
    },
    getScrollPercent() {
      var h = document.documentElement,
        b = document.body,
        st = "scrollTop",
        sh = "scrollHeight";
      return ((h[st] || b[st]) / ((h[sh] || b[sh]) - h.clientHeight)) * 100;
    },
    emitInterface() {
      this.$emit("interface", {
        activatePopupEngines: (trg, occ) => this.activatePopupEngines(trg, occ),
      });
    },
  },
  mounted() {
    // Emits on mount
    this.emitInterface();
  },
};
</script>

<style src="../../assets/css/elements/popup.css"></style>