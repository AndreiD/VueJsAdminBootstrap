<template>
  <v-app>
    <v-navigation-drawer dark mobile-break-point="800" width="240" app v-model="drawer">
      <v-list>
        <v-list-tile avatar>
          <v-list-tile-avatar>
            <img src="./assets/logo.png">
          </v-list-tile-avatar>
          <v-list-tile-content>
            <v-list-tile-title class="font-weight-bold">Jon Snow</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
      <v-list two-line>
        <v-list-tile v-for="(item, index) in items" :key="index" :to="item.path">
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-html="item.title"></v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar flat fixed app>
      <v-toolbar-side-icon @click="drawer = !drawer;"></v-toolbar-side-icon>
      <v-toolbar-title>
        <span class="font-weight-bold">Awesome</span>App
      </v-toolbar-title>
    </v-toolbar>
    <v-content class="mt-5 mx-4 mb-4">
      <v-container fluid fill-height>
        <v-layout justify-center align-center>
          <v-flex xs12 md6>
            <transition name="fade" mode="out-in">
              <router-view></router-view>
            </transition>
          </v-flex>
        </v-layout>
        <v-snackbar v-model="snackbar.visible" bottom>
          {{ snackbar.message }}
          <v-btn @click="snackbar.visible = !snackbar.visible;">Close</v-btn>
        </v-snackbar>
      </v-container>
    </v-content>
    <v-footer class="px-3 d-flex justify-content-between grey--text" app>
      <span>Copyright Me &copy; 2019 - present</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      drawer: true,
      url: "",
      busy: false,
      rating: 0,
      snackbar: {
        visible: false,
        message: ""
      },
      items: [
        {
          path: "/",
          title: "Home",
          icon: "fa-home"
        },
        {
          path: "/login",
          title: "Sign In",
          icon: "fa-sign-in-alt"
        },
        {
          path: "/about",
          title: "About",
          icon: "fa-info"
        },
        {
          path: "/faq",
          title: "FAQ",
          icon: "fa-question"
        },
        {
          path: "/logout",
          title: "Sign Out",
          icon: "fa-sign-out-alt"
        }
      ],
      right: null
    };
  }
};
</script>



<style type="text/css">
.v-content {
  padding: 0 20px 50px;
  background-color: #fefefe;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.loading:after {
  content: " .";
  animation: dots 1s steps(5, end) infinite;
}

@keyframes dots {
  0%,
  20% {
    color: rgba(0, 0, 0, 0);
    text-shadow: 0.25em 0 0 rgba(0, 0, 0, 0), 0.5em 0 0 rgba(0, 0, 0, 0);
  }
  40% {
    color: black;
    text-shadow: 0.25em 0 0 rgba(0, 0, 0, 0), 0.5em 0 0 rgba(0, 0, 0, 0);
  }
  60% {
    text-shadow: 0.25em 0 0 black, 0.5em 0 0 rgba(0, 0, 0, 0);
  }
  80%,
  100% {
    text-shadow: 0.25em 0 0 black, 0.5em 0 0 black;
  }
}
</style>
