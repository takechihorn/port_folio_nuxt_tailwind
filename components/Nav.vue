<template>
<div>
  <div>
    <div class="antialiased bg-gray-100 dark-mode:bg-gray-900">
      <div class="w-full text-gray-700 bg-white dark-mode:text-gray-200 dark-mode:bg-gray-800">
        <div class="flex flex-col px-2 mx-auto">
          <div class="flex flex-row items-center justify-between p-4">
            <a href="/" class="text-lg font-semibold tracking-widest text-gray-900 uppercase rounded-lg dark-mode:text-white focus:outline-none focus:shadow-outline">SHARE MEMORIES</a>
          <ul class="flex justify-end">
            <li class="mr-6" v-if="!this.$store.getters['auth/user']">
              <router-link to="/login" >
                <a class="btn text-primary border-primary md:border-2 hover:bg-primary hover:text-white transition ease-out duration-500">Login</a>
              </router-link>
            </li>
            <li class="mr-6" v-if="!this.$store.getters['auth/user']">
        <router-link to="/register" >
          <a class="btn text-primary border-primary md:border-2 hover:bg-primary hover:text-white transition ease-out duration-500"
            >Sign Up</a
          >
        </router-link>
      </li>
            <li class="mr-6" v-if="this.$store.getters['auth/user']">
          <a class="pl-2 text-primary"
            >Welcome {{ $auth.email }}</a
          >
      </li>
      <li class="mr-6" v-if="this.$store.getters['auth/user']">
              <router-link to="/" >
                <a class="btn text-primary border-primary md:border-2 hover:bg-primary hover:text-white transition ease-out duration-500">Top</a>
              </router-link>
            </li>
            <li class="mr-6" v-if="this.$store.getters['auth/user']">
        <router-link to="/albums" >
          <a class="btn text-primary border-primary md:border-2 hover:bg-primary hover:text-white transition ease-out duration-500"
            >Albums</a
          >
        </router-link>
      </li>
      <li class="mr-6" v-if="this.$store.getters['auth/user']">
        <div>
          <a class="btn text-primary border-primary md:border-2 hover:bg-primary hover:text-white transition ease-out duration-500"
          @click="logout"
            >Logout</a
          >
        </div>
      </li>
          </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  mounted(){
    console.log(this.$store.getters['auth/user'])
  },
  methods: {
    async logout(){
      await this.$store.dispatch("auth/logout")
      this.$router.push("/")
    }
  }
}
</script>

<style>

</style>
