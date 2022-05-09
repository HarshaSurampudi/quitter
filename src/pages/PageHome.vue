<template>
  <q-page class="">
    <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
      <div class="col">
        <q-input
          filled
          bottom-slots
          v-model="newQuitContent"
          placeholder="What's happening?"
          counter
          maxlength="280"
          bg-color="white"
          autogrow
          class="new-quit"
        >
          <template v-slot:before>
            <q-avatar size="xl">
              <img src="https://cdn.quasar.dev/img/avatar5.jpg" />
            </q-avatar>
          </template>
        </q-input>
      </div>
      <div class="col col-shrink">
        <q-btn
          :disabled="!newQuitContent"
          no-caps
          unelevated
          rounded
          color="primary"
          label="Quit"
          class="q-mb-lg"
          @click="addNewQuit"
        />
      </div>
    </div>
    <q-separator size="10px" color="grey-2" class="divider" />

    <q-list class="" separator>
      <transition-group
        appear
        enter-active-class="animated bounceIn slower"
        leave-active-class="animated bounceOut slower"
      >
        <q-item class="q-py-md" v-for="quit in quits" :key="quit.date">
          <q-item-section avatar top>
            <q-avatar size="xl">
              <img src="https://cdn.quasar.dev/img/avatar5.jpg" />
            </q-avatar>
          </q-item-section>

          <q-item-section>
            <q-item-label class="text-subtitle1"
              ><strong>Harsha Surampudi</strong
              ><span class="text-grey-7">@harsha1428</span></q-item-label
            >
            <q-item-label class="quit-content text-body1">
              {{ quit.content }}
            </q-item-label>
            <div class="row justify-between q-mt-sm quit-icons">
              <q-btn color="grey" size="sm" icon="far fa-comment" flat round />
              <q-btn color="grey" size="sm" icon="fas fa-retweet" flat round />
              <q-btn color="grey" size="sm" icon="far fa-heart" flat round />
              <q-btn
                @click="deleteQuit(quit)"
                color="grey"
                size="sm"
                icon="fas fa-trash"
                flat
                round
              />
            </div>
          </q-item-section>

          <q-item-section side top>
            {{ relativeDate(quit.date) }}
          </q-item-section>
        </q-item>
      </transition-group>
    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import { formatDistance } from "date-fns";

export default defineComponent({
  name: "PageHome",
  data() {
    return {
      newQuitContent: "",
      quits: [
        {
          content:
            "Joy is what happens to us when we allow ourselves to recognize how good things really are.",
          date: 1652115587940,
        },
        {
          content:
            "I am not bothered by the fact that I am unknown. I am bothered when I do not know others.",
          date: 1652115614138,
        },
      ],
    };
  },

  methods: {
    relativeDate(value) {
      return formatDistance(value, new Date());
    },
    addNewQuit() {
      let newQuit = {
        content: this.newQuitContent,
        date: Date.now(),
      };
      this.quits.unshift(newQuit);
      this.newQuitContent = "";
    },
    deleteQuit(quit) {
      let dateToDelete = quit.date;
      let index = this.quits.findIndex((quit) => quit.date === dateToDelete);
      this.quits.splice(index, 1);
    },
  },
});
</script>

<style lang="sass">
.new-quit
  textarea
    font-size: 19px
    line-height: 1.4 !important
.divider
  border-top: 1px solid
  boder-bottom: 1px solid
  border-color: $grey-4
.quit-content
  white-space: pre-line

.quit-icons
  margin-left: -5px
</style>
