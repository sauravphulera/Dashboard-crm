<script>
import SideNav from './SideNav.vue';
import SideBar from './SideBar.vue';
import { DOCTABLEDATA, DOCTABLEHEADERS, SIDEBARDATA, SIDENAVCONTENT } from '../constants/constants';
import SvgIcon from '@jamescoyle/vue-icon';
import { mdiBellOutline, mdiTrendingUp } from '@mdi/js';

//graphs
import { Line, Bar } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale, PointElement, LineElement } from 'chart.js'
ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale, PointElement, LineElement)

const labels = ['Jan','Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov','Dec'];
const data = {
  labels: labels,
  datasets: [{
    label: 'My First Dataset',
    data: [42, 50,55,60, 80, 81, 56, 55,75,67,77,65,55,78, 40,20],
    fill: false,
    borderColor: 'rgb(75, 192, 192)',
    backgroundColor: 'rgb(75, 192, 192)',
    tension: 0.1
  }]
};
export default {
  name: 'Dashboard',
  data() {
    return {
          path: mdiBellOutline,
          tradeUp: mdiTrendingUp,
          sideNavContent: SIDENAVCONTENT,
          lineChartData: data,
          chartOptions: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: {
                  display: false
                }
            },
            scales: {
              x: {
                display: true,
                grid: {
                  display: false
                },
                barThickness: 1
              },
              y: {
                display: false,
              },
              
            }
          },
          doctHeaders: DOCTABLEHEADERS,
          docTableData: DOCTABLEDATA,
          sideBarData: SIDEBARDATA,
      }
    
  },
  components: {
    SideNav,
    SvgIcon,
    Line,
    Bar,
    SideBar,
  },
  mounted() {
      
  }
}
</script>

<template>
  <div class="head-container">
      <div class="side-nav">
        <SideNav :navData="{...sideNavContent}"/>
      </div>
      <div class="dash-container">
          <div class="dashboard">

            <!--top heading and notif-->
              <div class="flex justify-between w100">
                  <div class="fw700 fs-24">OverView</div>
                  <div><svg-icon type="mdi" :path="path"></svg-icon></div>
              </div>

              <!--upper cards-->
              <div class="flex space around mt20 gap24">
                  <div class="card">
                      <div class="flex w100 space-between">
                          <div class="fw500">Document</div>
                          <div class="card-icon-container flex align-center justify-center"><svg-icon type="mdi" :path="path"></svg-icon></div>
                      </div>
                      <div class="fw700 fs-24 mt32">146.0000</div>
                      <div class="flex mt32 space-around">
                          <div class="flex pr-12 estimate-profit-text"><svg-icon type="mdi" :path="tradeUp"></svg-icon>17%</div>
                          <div class="sub-txt">Since last week</div>
                      </div>
                  </div>
                  <div class="card">
                      <div class="flex w100 space-between">
                          <div class="fw500">Contact</div>
                          <div class="card-icon-container flex align-center justify-center"><svg-icon type="mdi" :path="path"></svg-icon></div>
                      </div>
                      <div class="fw700 fs-24 mt32">1400</div>
                      <div class="flex mt32 space-around">
                          <div class="flex pr-12 estimate-profit-text"><svg-icon type="mdi" :path="tradeUp"></svg-icon>17%</div>
                          <div class="sub-txt">Since last week</div>
                      </div>
                  </div>
                  <div class="card">
                      <div class="flex w100 space-between">
                          <div class="fw500">Email</div>
                          <div class="card-icon-container flex align-center justify-center"><svg-icon type="mdi" :path="path"></svg-icon></div>
                      </div>
                      <div class="fw700 fs-24 mt32">152.700</div>
                      <div class="flex mt32 space-around">
                          <div class="flex pr-12 estimate-profit-text">
                            <svg-icon type="mdi" :path="tradeUp">
                            </svg-icon>
                            17%
                          </div>
                          <div class="sub-txt">Since last week</div>
                      </div>
                  </div>
              </div>
              <!--middle cards-->
              <div class="flex space-around gap24 mt24">

                    <!--line chart-->
                    <div class="card">
                          <div class="fw500">Recent Workflow</div>
                          <div class="flex w100">
                              <div class="mt20 flex pr-12 estimate-profit-text"><svg-icon type="mdi" :path="tradeUp"></svg-icon>17%</div>
                              <v-container class="chart-container w100">
                                <Line
                                  :style="{height: '250px', position: 'relative'}"
                                  class="w100"
                                  id="my-chart-id"
                                  :options="chartOptions"
                                  :data="lineChartData"
                                />
                              </v-container>

                          </div>

                          
                    </div>

                    <!--bar chart-->
                    <div class="card">
                      <div class="fw500">Recent Marketing</div>
                      <div class="flex w100">
                          <div class="mt20 flex pr-12 estimate-profit-text"><svg-icon type="mdi" :path="tradeUp"></svg-icon>17%</div>
                          <v-container class="chart-container w100">
                            <Bar class="w100"
                            :style="{height: '250px', position: 'relative'}"
                                id="my-chart-id"
                                :options="chartOptions"
                                :data="lineChartData"
                            />
                          </v-container>

                      </div>

                    </div>
              </div>

            
              <!--lower cards-->
              <div class="flex gap24 mt24">
                  <div class="card">
                      <div class="flex space-between">
                          <div class="fw500">Document</div>
                          <div>
                              <select name="Months" id="months">
                                  <option value="audi">Daily</option>
                                  <option value="volvo">Weekly</option>
                                  <option value="saab">Monthly</option>
                                  <option value="mercedes">Yearly</option>
                              </select>
                          </div>
                      </div>
                      <div class="sub-txt">Document tracking information</div>

                      <!--table-->
                      <div>
                          <table class="doc-table mt24 w100">
                            <thead>
                              <td v-for="(header, i) in this.doctHeaders" :key="`key-${i}`" class="thead fw700">
                                <span :style="{ 'color': header === 'Status' ? 'rgb(162 168 172)': 'black' }">{{ header }}</span>
                                
                              </td>
                            </thead>
                            <tbody>
                              <tr v-for="(item, i) in this.docTableData" :key="`key-${i}`">
                                <td class="tdata" v-for="(header, i) in this.doctHeaders" :key="`key-${i}`">
                                  <span v-if="header !== 'Status'">{{ item[header] }}</span>
                                  <span v-if="header === 'Status'">
                                    <button class="action-btn" :class="item[header]">{{ item[header] }}</button>
                                  </span>
                                </td>
                              </tr>
                            </tbody>
                          </table>
                      </div>

                  </div>
              </div>
          </div>
          <div class="sidebar">
            <div class="flex">
                <div class="profile flex align-center justify-center mr8">
                  <div>A</div>
                </div>
                <div>
                  <select name="admin" id="admin" class="user-select">
                                  <option value="audi">Administration</option>
                                  <option value="volvo">User 1</option>
                   </select>
                </div>
            </div>
            <div class="w100 mt12">
              <SideBar :data="{...sideBarData}" />
            </div>
          </div>
      </div>
  </div>
</template>



<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.chart-container {
  position: relative;
  margin: auto;
  /*height: 30vh;*/
  width: 20vw;
}
.user-select {
  background: transparent;
    font-weight: 700;
    color: #3c3b3b;
    
}

.sidebar {
  padding: 1em;
  height: calc(100% - 3em);
}

.send {
  color: rgb(8, 97, 8);
  background: #d1f4d1;
}
.pending {
  color: rgb(204 57 17);
    background: rgb(255 224 216);
}
.doc-table td{
  padding: 16px 0;
}
.chart-container {
  flex-grow: 1;
  min-height: 0;
  min-width: 0;
}

  .head-container {
    display: flex;
    height: 100%;
    min-height: 720px;
  }
  .side-nav {
    /*height: 100%;*/
    max-width: 280px;
    width: -webkit-fill-available;
  }
  .dash-container {
    width: 100%;
    height: 100%;
    display: flex;
    background-color: lightgray;
  }
  .dashboard {
    width: 88%;
    height: calc(100% - 3em);
    padding: 1em;
  }
  .sidebar {
    width: 22%;
    /*min-width: 270px;*/
    height: 100%;
  }
  .card {
    background: white;
    padding: 24px;
    border-radius: 8px;
    flex:1;
  }
  .card-icon-container {
    background: #e3f5ff;
    border-radius: 50%;
    width: 45px;
    height: 45px;
    color: #009dee;
  }
  .estimate-profit-text {
    color:  #1ec11e;
  }
</style>
