<script setup>
import FriendsIcon from './components/icons/navbar/IconFriends.vue'
import HomeIcon from './components/icons/navbar/IconHome.vue'
import SettingsIcon from './components/icons/navbar/IconSettings.vue'
import ProfileIcon from './components/icons/navbar/IconProfile.vue'

// For testing queries of the database the little button in the left corner
// THIS CAN BE DELETED AFTER THE APP IS FINISHED
import { VueQueryDevTools } from "vue-query/devtools";
import { useQueryProvider } from 'vue-query';
import { onBeforeMount } from 'vue'
import { useStore } from 'vuex'

const store = useStore()

onBeforeMount(() => {
  store.dispatch('fetchUser')
})
useQueryProvider();
</script>

<template>
  <main>
    <nav>
      <ul>
        <HomeIcon />
        <ProfileIcon />
        <FriendsIcon />
        <SettingsIcon />
      </ul>
    </nav>
  </main>

  <router-view></router-view>
  <VueQueryDevTools :initialIsOpen="false" />
</template>


<style>
/* @import './assets/base.css'; */
* {
  margin: 0;
  padding: 0;
}
#app {
  font-weight: normal;
  /* iphone 13 mini height and width*/
  height: 812px;
  width: 375px;
  position: relative;
}

main {

}

nav {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 70px;
background: linear-gradient(180.7deg, #FFFFFF 0.61%, #8A8A8A 75.57%);
  opacity: 1;
  z-index: 1;
}




nav ul {
  display: grid;
  grid-auto-columns: 1fr;
  grid-auto-flow: column;
  margin: 0%;
  margin-left: 45px;
  margin-top: 0.6cm;
  align-items: center;
  z-index: 1;
}

</style>


