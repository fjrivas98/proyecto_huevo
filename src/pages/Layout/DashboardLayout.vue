<template>
  <div class="wrapper" :class="{ 'nav-open': $sidebar.showSidebar }">
    <notifications></notifications>

    <side-bar
      :sidebar-item-color="sidebarBackground"
      :sidebar-background-image="sidebarBackgroundImage"
    >
      <mobile-menu slot="content"></mobile-menu>
      <!-- <sidebar-link to="/dashboard">
        <md-icon>dashboard</md-icon>
        <p>Bases de Datos</p>
      </sidebar-link> -->
      <sidebar-link to="/databases">
        <md-icon>databases</md-icon>
        <p>Bases de Datos</p>
      </sidebar-link>
      <sidebar-link to="/user">
        <md-icon>person</md-icon>
        <p>Usuarios</p>
      </sidebar-link>
      <sidebar-link to="/table">
        <md-icon>content_paste</md-icon>
        <p>Tablas</p>
      </sidebar-link>
      <sidebar-link to="/typography">
        <md-icon>library_books</md-icon>
        <p>Información</p>
      </sidebar-link>
      <sidebar-link to="/icons">
        <md-icon>bubble_chart</md-icon>
        <p>Kenosementiende</p>
      </sidebar-link>
      <a href="http://localhost/proyecto/proyecto/public/import.php" class="MyBoton">Importar</a>
    </side-bar>

    <div class="main-panel">
      <top-navbar></top-navbar>

    

      <dashboard-content> </dashboard-content>

      <content-footer v-if="!$route.meta.hideFooter"></content-footer>
    </div>
  </div>
</template>

<script>
const $ = require('jquery')

import TopNavbar from "./TopNavbar.vue";
import ContentFooter from "./ContentFooter.vue";
import DashboardContent from "./Content.vue";
import MobileMenu from "@/pages/Layout/MobileMenu.vue";

export default {
  components: {
    TopNavbar,
    DashboardContent,
    ContentFooter,
    MobileMenu
  },
  data() {
    return {
      sidebarBackground: "green",
      sidebarBackgroundImage: require("@/assets/img/sidebar-2.jpg")
    };
  },
  // methods: {
  //   onClickButton () {
  //     location.href = 'http://localhost/proyecto/proyecto/public/import.php'
  //   }
  // }
};


</script>
<style>
  .MyBoton {
background-color:transparent;
	border-radius:4px;
	display:inline-block;
	cursor:pointer;
	color:#ffffff;
	font-family:Trebuchet MS;
	font-size:13px;
	font-weight:bold;
	padding:15px 76px;
	text-decoration:none;
}

</style>
