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
      <!-- after login -->
      <v-menu
        v-if="isLogin"
        offset-y
        transition="slide-y-transition"
      >
        <template v-slot:activator="{ on }">
          <v-btn icon v-on="on">
            <v-icon>face</v-icon>
          </v-btn>
        </template>
        <v-list>
          <v-list-tile>
            <v-list-tile-content>
              <v-list-tile-title>내 정보</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-divider></v-divider>
          <v-subheader>크리에이터</v-subheader>
          <v-list-tile>
            <v-list-tile-content>
              <v-list-tile-title>채용공고 등록</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile>
            <v-list-tile-content>
              <v-list-tile-title>채용공고 관리</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-divider></v-divider>
          <v-subheader>에디터</v-subheader>
          <v-list-tile>
            <v-list-tile-content>
              <v-list-tile-title>지원서 관리</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile>
            <v-list-tile-content>
              <v-list-tile-title>지원 현황</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-divider></v-divider>
          <v-list-tile @click="logout">
            <v-list-tile-content>
              <v-list-tile-title>로그아웃</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
      </v-menu>
      <!-- before login -->
      <v-menu
        v-else
        offset-y
        transition="slide-y-transition"
      >
        <template v-slot:activator="{ on }">
          <v-btn icon v-on="on">
            <v-icon>person</v-icon>
          </v-btn>
        </template>
        <v-list>
          <v-list-tile @click="loginDialog['isShow'] = true">
            <v-list-tile-title>회원가입 | 로그인</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-menu>
    </v-toolbar>
    <v-content>
      <v-container fluid fill-height>
        <v-layout justify-center align-center class="text-xs-center">
          <router-view></router-view>
        </v-layout>
      </v-container>
    </v-content>
    <!-- login dialog -->
    <v-dialog v-model="loginDialog['isShow']" width="400px">
      <v-card>
        <v-card-title>
          <v-layout wrap column class="text-xs-center">
            <span class="headline font-weight-bold">크루크루</span>
          </v-layout>
        </v-card-title>
        <v-card-text>
          <v-container pt-0>
            <v-layout wrap column class="text-xs-center">
              <div><b>YouTube</b> 크리에이터 `크루` 결성을 도와드립니다.</div>
              <div>지금 바로 크루크루 서비스를 이용해보세요 :)</div>
              <v-img
                :src="require('@/assets/google.png')"
                contain
                height="50"
                class="ma-4"
                @click="login"
                style="cursor: pointer;"
              ></v-img>
              <small>회원가입시 <span class="primary--text">서비스 이용약관</span>과 <span class="primary--text">개인정보 취급방침</span>을 읽고 동의했습니다.</small>
            </v-layout>
          </v-container>
        </v-card-text>
      </v-card>
    </v-dialog>
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
      isLogin: false,
      loginDialog: {
        'isShow': false,
      },
    }
  },
  methods: {
    changeMenu (name) {
      this.$router.push({ 'name': name })
    },
    login () {
      this.isLogin = true
      this.loginDialog['isShow'] = false
    },
    logout () {
      this.isLogin = false
    },
  },
}
</script>
