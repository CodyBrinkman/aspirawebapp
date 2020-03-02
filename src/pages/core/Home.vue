<!-- Issues:
  * Image alignment - Crop!
 -->
<template>
  <v-container fluid>
    <v-layout row>
      <v-flex md1>
        <v-avatar>
          <img src="@/assets/icons/availity.png" />
        </v-avatar>
      </v-flex>
    </v-layout>
    <v-layout row>
      <v-flex md6 class="text-position">
        <p class="text-style font-weight-bold">
          There are many ways to
          <br />live a healthy life. We help you
          <br />find yours.
        </p>
      </v-flex>
    </v-layout>
    <v-layout row>
      <v-flex md6 class="text-position">
        <p class="text-style-1 font-weight-bold">Select your payer to login.</p>
      </v-flex>
    </v-layout>
    <v-layout row class="first-row-position">
      <v-flex md1>
        <v-hover v-slot:default="{ hover }">
          <v-card :elevation="hover ? 12 : 2" width="130">
            <v-avatar class="profile" color="white" size="130" tile @click="login">
              <v-img :src="require('@/assets/payers/aspira.png')" />
            </v-avatar>
          </v-card>
        </v-hover>
      </v-flex>
      <v-flex md1 class="position">
        <v-hover v-slot:default="{ hover }">
          <v-card :elevation="hover ? 12 : 2" width="130">
            <v-avatar class="profile" color="white" size="130" tile>
              <v-img :src="require('@/assets/payers/careplus.jpg')" />
            </v-avatar>
          </v-card>
        </v-hover>
      </v-flex>
      <v-flex md1 class="position">
        <v-hover v-slot:default="{ hover }">
          <v-card :elevation="hover ? 12 : 2" width="130">
            <v-avatar class="profile" color="white" size="130" tile>
              <v-img :src="require('@/assets/payers/ccs.jpg')" />
            </v-avatar>
          </v-card>
        </v-hover>
      </v-flex>
      <v-flex md1 class="position">
        <v-hover v-slot:default="{ hover }">
          <v-card :elevation="hover ? 12 : 2" width="130">
            <v-avatar class="profile" color="white" size="130" tile>
              <v-img :src="require('@/assets/payers/cigna.png')" />
            </v-avatar>
          </v-card>
        </v-hover>
      </v-flex>
      <v-flex md1 class="position">
        <v-hover v-slot:default="{ hover }">
          <v-card :elevation="hover ? 12 : 2" width="130">
            <v-avatar class="profile" color="white" size="130" tile>
              <v-img :src="require('@/assets/payers/CMS.jpg')" />
            </v-avatar>
          </v-card>
        </v-hover>
      </v-flex>
      <v-flex md1 class="position">
        <v-hover v-slot:default="{ hover }">
          <v-card :elevation="hover ? 12 : 2" width="130">
            <v-avatar class="profile" color="white" size="130" tile>
              <v-img :src="require('@/assets/payers/flblue.png')" />
            </v-avatar>
          </v-card>
        </v-hover>
      </v-flex>
    </v-layout>
    <v-layout row class="second-row-position">
      <v-flex md1>
        <v-hover v-slot:default="{ hover }">
          <v-card :elevation="hover ? 12 : 2" width="130">
            <v-avatar class="profile" color="white" size="130" tile>
              <v-img :src="require('@/assets/payers/flmedicaid.jpg')" />
            </v-avatar>
          </v-card>
        </v-hover>
      </v-flex>
      <v-flex md1 class="position">
        <v-hover v-slot:default="{ hover }">
          <v-card :elevation="hover ? 12 : 2" width="130">
            <v-avatar class="profile" color="white" size="130" tile>
              <v-img :src="require('@/assets/payers/leon.png')" />
            </v-avatar>
          </v-card>
        </v-hover>
      </v-flex>
      <v-flex md1 class="position">
        <v-hover v-slot:default="{ hover }">
          <v-card :elevation="hover ? 12 : 2" width="130">
            <v-avatar class="profile" color="white" size="130" tile>
              <v-img :src="require('@/assets/payers/prestige.png')" />
            </v-avatar>
          </v-card>
        </v-hover>
      </v-flex>
      <v-flex md1 class="position">
        <v-hover v-slot:default="{ hover }">
          <v-card :elevation="hover ? 12 : 2" width="130">
            <v-avatar class="profile" color="white" size="130" tile>
              <v-img :src="require('@/assets/payers/sunshine.png')" />
            </v-avatar>
          </v-card>
        </v-hover>
      </v-flex>
      <v-flex md1 class="position">
        <v-hover v-slot:default="{ hover }">
          <v-card :elevation="hover ? 12 : 2" width="130">
            <v-avatar class="profile" color="white" size="130" tile>
              <v-img :src="require('@/assets/payers/unicare.png')" />
            </v-avatar>
          </v-card>
        </v-hover>
      </v-flex>
      <v-flex md1 class="position">
        <v-hover v-slot:default="{ hover }">
          <v-card :elevation="hover ? 12 : 2" width="130">
            <v-avatar class="profile" color="white" size="130" tile>
              <v-img :src="require('@/assets/payers/wellcare.png')" />
            </v-avatar>
          </v-card>
        </v-hover>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      loading: false,
      userEmail: "test",
      password: "test",
      hidePassword: true,
      error: false,
      showResult: false,
      result: "",
      rules: {
        required: value => !!value || "Required."
      }
    };
  },

  methods: {
    login() {
      const vm = this;

       {
        vm.$router.push({ name: "Login" });
      } 
    }
  }
};
</script>

<style scoped lang="css">
@import url("https://fonts.googleapis.com/css?family=Poppins");
.container {
  background-image: url("~@/assets/icons/humana_bg.png");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  height: 101vh;
  overflow: auto;
}
.text-position {
  margin-top: 2%;
  margin-left: 5%;
}
.text-style {
  font-size: 43px;
  font-family: "Roboto", sans-serif;
  color: rgb(78, 129, 56);
  line-height: 120%;
}
.text-style-1 {
  font-size: 20px;
  font-family: "Roboto", sans-serif;
  line-height: 120%;
  font-weight: 500;
}
.position {
  margin-left: 5%;
}
.first-row-position {
  margin-left: 5%;
}
.second-row-position {
  margin-left: 5%;
  margin-top: 5%;
}
</style>
