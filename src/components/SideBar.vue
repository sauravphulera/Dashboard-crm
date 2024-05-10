<template>
	<div class="sidebar-container card">
		<div class="p-column" v-for="(item, index) in this.headers" :key="`ID-${index}`">
        <div class="sub-header">{{ item }}</div>
        <div class="flex align-center sub-heading-container" v-for="(subItem, i) in this.data[item]" :key="`ID-${i}`">
			<div class="flex align-center w100">
				<div class="profile mr16"></div>
				<div>
					<div class="sub-link">
						{{ subItem.name }}
					</div>
					<div class="sub-txt pt-4">
						{{ subItem.description }}
					</div>
				</div>

			</div>
        </div>
    </div>
	</div>
</template>
  
  <script>
  
  export default {
	name: 'SideBar',
	data() {
    return {
        headers: []
      }
    
  },
  props: ['data'],
  mounted () {
    console.log(this.data);
    this.headers = Object.keys({...this.data});
    console.log(this.headers)
  },
  }
  </script>
  
  <style scoped>
  .sidebar-container {
    background: white;
    padding: 24px;
    border-radius: 8px;
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