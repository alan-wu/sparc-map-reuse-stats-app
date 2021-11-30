<template>
  <el-container class="container">
    <el-header class="header" height="40px">MapClient download stats</el-header>
      <el-table
        :data="mapclientStats"
        style="width: 100%">
        <el-table-column
          prop="published"
          label="Published Date"
          width="180">
        </el-table-column>
        <el-table-column
          prop="tag"
          label="Tag"
          width="100">
        </el-table-column>
        <el-table-column
          prop="name"
          label="Name"
          width="180">
        </el-table-column>
        <el-table-column
          prop="download"
          label="Download Count"
          width="100">
        </el-table-column>
      </el-table>
  </el-container>
</template>

<script>
/* eslint-disable no-alert, no-console */
import Vue from "vue";
import { Container, Header, Icon, Main,  Table, TableColumn } from "element-ui";
import lang from "element-ui/lib/locale/lang/en";
import locale from "element-ui/lib/locale";
locale.use(lang);
Vue.use(Container);
Vue.use(Header);
Vue.use(Icon);
Vue.use(Main);
Vue.use(Table);
Vue.use(TableColumn);

export default {
  name: "MapReuseStatsPage",
  data: function() {
    return {
      mapclientStats: []
    };
  },
  created: function() {
    fetch("https://api.github.com/repos/MusculoskeletalAtlasProject/mapclient/releases")
    .then(
      response => {
        if (response.status !== 200) {
          console.log('Encounter a problem: ' +
            response.status);
          return;
        }
        // Examine the text in the response
        response.json().then(data => {
          console.log(data)
          data.forEach(element =>{
            element.assets.forEach(asset => {
              let item = {};
              item.tag = element.tag_name;
              item.name = asset.name;
              item.download = asset.download_count;
              item.published = element.published_at;
              this.mapclientStats.push(item);
            });
           
          });
        });
      }
    )
    .catch(err => {
      console.log('Fetch Error :-S', err);
    });
  }
};
</script>

<!-- Add "scop  height:40px; to this component only -->


<style scoped lang="scss">
@import "~element-ui/packages/theme-chalk/src/container";
@import "~element-ui/packages/theme-chalk/src/header";
@import "~element-ui/packages/theme-chalk/src/main";
@import "~element-ui/packages/theme-chalk/src/table";
@import "~element-ui/packages/theme-chalk/src/table-column";

.container {
  text-align: justify;
  width: 100%;
  border-radius: 4px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  padding: 1em;
  background: #fff;
  height:100%;
}

</style>
