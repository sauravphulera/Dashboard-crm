<script>
import SvgIcon from '@jamescoyle/vue-icon';
import { mdiViewDashboardOutline } from '@mdi/js';
export default {
  name: 'SideNav',
  data() {
    return {
        path: mdiViewDashboardOutline,
        headers: []
      }
    
  },
  props: ['navData'],
  mounted () {
    console.log(this.navData);
    this.headers = Object.keys({...this.navData});
    console.log(this.headers)
  },
  components: {
    SvgIcon
  }
}
</script>

<template>
  <div class="sidenav-container">
	 <div class="nav-header">
		<div class="logo p-column">CRM.io</div>

    <!--header-->
		<div class="flex p-column align-center selected">
			<svg-icon class="pr-6" type="mdi" :path="path"></svg-icon>
			<div>Dashboard</div>
		</div>
      <!--nav content-->
    <div class="p-column" v-for="(item, index) in this.headers" :key="`ID-${index}`">
        <div class="sub-header">{{ item }}</div>
        <div class="flex align-center sub-heading-container" v-for="(subLinks, i) in this.navData[item]" :key="`ID-${i}`">
            <svg-icon class="pr-6" type="mdi" :path="path"></svg-icon>
            <div class="sub-link">
               {{ subLinks.name }}
            </div>
        </div>
        <div v-if="index < this.headers.length - 1" class="line"></div>
    </div>
    <div>

    </div>
	 </div>
  </div>
</template>



<style scoped>
  .sidenav-container {
    width: 100%;
    max-width: 248px;
    padding: 16px;
    background: #0c1b32;
    color: lightgrey;
    height: calc(100% - 32px);
  }
  .logo {
	font-size: 20px;
    font-style: oblique;
    font-family: monospace;
    color: #ff8600;
  }
  .p-column {
	padding: 1em 1em 1em 2em;
  }
  .icon {
	height: 35px;
	width: 35px;
	color: white;
	background: white;
  }

  .selected {
    background: #029dcf;
    color: white;
    border-radius: 12px;
  }

  .nav-header {
    width:100%;
  }
  .sub-link {
    font-size: 14px;
    font-weight: 500;
  }
  .sub-header {
    font-weight: 600;
    color: #00599b;
  }
  .line {
    border-bottom: 1px solid white;
  }
  .sub-heading-container {
    padding: 1em 0;
    color: #6ca4b5;
  }
</style>
