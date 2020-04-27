<template>
  <v-app dark>

    <Navbar 
      :title="title" 
      @toggle-left-mini="miniVariant = !miniVariant" 
      @toggle-left-clipped="clipped = !clipped" 
      @toggle-left-drawer="leftDrawer = !leftDrawer" 
      @toggle-right-drawer="rightDrawer =!rightDrawer"  
    />

    <v-navigation-drawer v-model="leftDrawer" :mini-variant="miniVariant" :clipped="clipped" fixed app>
      <v-list>
        <v-list-item v-for="(item, i) in items" :key="i" :to="item.to" router exact>
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>

    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon>mdi-repeat</v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-footer :fixed="fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import Navbar from "@/components/Navbar.vue";

export default {
  components: {
    Navbar
  },
  data() {
    return {
      title: "Nuxt-Vuetify",
      clipped: false,
      fixed: false,
      miniVariant: false,
      right: true,
      leftDrawer: false,  
      rightDrawer: false,    
      items: [
        {
          icon: "mdi-apps",
          title: "Welcome",
          to: "/"
        },
        {
          icon: "mdi-information",
          title: "About",
          to: "/about"
        },
        {
          icon: "mdi-chart-bubble",
          title: "Inspire",
          to: "/inspire"
        }
      ]      
    };
  }
};
</script>
