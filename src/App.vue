<template>
  <v-app app>
    <v-navigation-drawer
      v-model="drawer"
      :clipped="$vuetify.breakpoint.lgAndUp"
      app fixed
    >
      <v-list>
        <v-subheader>크리에이터</v-subheader>
        <v-list-tile @click="changeMenu('home')">
          <v-list-tile-action>
            <v-icon>trending_up</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>유튜브 랭킹</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-subheader>에디터</v-subheader>
        <v-list-tile @click="changeMenu('about')">
          <v-list-tile-action>
            <v-icon>assignment_ind</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>채용공고</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-subheader>게시판</v-subheader>
        <v-list-tile>
          <v-list-tile-action>
            <v-icon>list</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>자유게시판</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile>
          <v-list-tile-action>
            <v-icon>announcement</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>공지사항</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile>
          <v-list-tile-action>
            <v-icon>hearing</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>서비스 문의</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar
      :clipped-left="$vuetify.breakpoint.lgAndUp" 
      app color="primary" dark fixed 
    >
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title>크루크루</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>person</v-icon>
      </v-btn>
    </v-toolbar>
    <v-content>
      <v-container fluid fill-height>
        <v-layout justify-center align-center class="text-xs-center">
          <router-view></router-view>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  created () {
    this.changeMenu('home')
  },
  data () {
    return {
      drawer: null,
    }
  },
  methods: {
    changeMenu (name) {
      this.$router.push({ 'name': name })
    },
  },
}
</script>
