<template>
  <div>
    <client-only>
      <v-app-bar :clipped-left="clipped" fixed dense app>

        <v-app-bar-nav-icon @click.stop="toggleLeftDrawer()" />

        <v-btn icon @click.stop="toggleLeftMini()">
          <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
        </v-btn>

        <v-btn icon @click.stop="toggleLeftClipped()">
          <v-icon>mdi-application</v-icon>
        </v-btn>

        <!--
        <v-btn icon @click.stop="fixed = !fixed">
          <v-icon>mdi-minus</v-icon>
        </v-btn>
        -->

        <v-toolbar-title v-text="theTitle" class="headline text-xs-center pa-2" />
        <v-spacer />

        <v-btn icon @click.stop="switchTheme()">
          <v-icon>mdi-brightness-6</v-icon>
        </v-btn>

        <v-btn icon @click.stop="toggleRightDrawer()">
          <v-icon>mdi-menu</v-icon>
        </v-btn>

      </v-app-bar>
    </client-only>
  </div>
</template>

<script>
export default {
  name: "toolbar", //for debugging in Vue-DevTools
  props: {
    title: {
      type: String,
      default: "",
      required: false
    }
  },
  data() {
    return {
      clipped: false,
      miniVariant: true,
      fixed: false,
      leftDrawer: false,
      rightDrawer: false,
      theTitle: ""
    };
  },
  created() {
    this.theTitle = this.title;
  },
  methods: {
    toggleLeftMini() {
      this.miniVariant = !this.miniVariant;
      //send notification to the parent:
      this.$emit("toggle-left-mini", this.clipped);
    },
    toggleLeftClipped() {
      this.clipped = !this.clipped;
      //send notification to the parent:
      this.$emit("toggle-left-clipped", this.clipped);
    },
    toggleLeftDrawer() {
      this.leftDrawer = !this.leftDrawer;
      //send notification to the parent:
      this.$emit("toggle-left-drawer", this.leftDrawer);
    },
    toggleRightDrawer() {
      this.rightDrawer = !this.rightDrawer; 
      //send notification to the parent:
      this.$emit("toggle-right-drawer", this.rightDrawer); 
    },
    switchTheme() {
      //https://medium.com/untitled-factory/advanced-color-management-in-vuetify-js-with-nuxt-js-6e20d26e37c6
      this.$vuetify.theme.isDark = !this.$vuetify.theme.isDark;
      console.log("clicked");
    }
  }
}
</script>