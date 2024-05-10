<template>
  <v-card rounded color="#EC9143" class="pa-7">
    <v-card-title>
      <v-row class="rowCard fontTitle" align="center">
        Welcome
      </v-row>
      <v-row class="rowCard fontTitle" align="center">
        Back
      </v-row>
    </v-card-title>
    <v-card-text>
      <v-row>
        <v-text-field v-model="email" rounded label="E-mail" outlined />
      </v-row>
      <v-row>
        <v-text-field v-model="password" rounded label="Password" outlined type="password" />
      </v-row>
    </v-card-text>
    <v-card-actions>
      <v-col cols="12">
        <v-row>
          <v-btn block class="pa-2" color="#134700" @click="login">
            <span style="text-transform: none; color: white;">Log-In</span>
          </v-btn>
        </v-row>
        <v-row class="rowCard">
          <span>If you Didn't have account</span>
          <a href="">Sign-Up</a>
        </v-row>
      </v-col>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
}
</script>

<style scoped>

</style>
