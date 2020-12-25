<template>
  <div>
    <div class="flex flex-col items-center flex-1 h-full justify-center px-4 py-40 sm:px-0">
        <div class="flex rounded-lg shadow-lg w-full sm:w-3/4 lg:w-1/2 bg-white sm:mx-0" style="height: 500px">
            <div class="flex flex-col w-full md:w-1/2 p-4">
                <div class="flex flex-col flex-1 justify-center mb-8">
                    <h1 class="text-4xl text-center font-thin">Welcome SignUp </h1>
                    <div class="w-full mt-4">
                        <form v-if="step == steps.register" @submit.prevent="register" class="form-horizontal w-3/4 mx-auto" method="POST" action="#">
                            <div class="flex flex-col mt-4">
                                <input v-model="registerForm.email" id="email" type="email" class="flex-grow h-8 px-2 border rounded border-grey-400" name="email" value="" placeholder="Email">
                            </div>
                            <div class="flex flex-col mt-4">
                                <input v-model="registerForm.password" id="password" type="password" class="flex-grow h-8 px-2 rounded border border-grey-400" name="password" required placeholder="Password">
                            </div>
                            <!-- <div class="flex items-center mt-4">
                                <input type="checkbox" name="remember" id="remember" class="mr-2"> <label for="remember" class="text-sm text-grey-dark">Remember Me</label>
                            </div> -->
                            <div class="flex flex-col mt-8">
                                <button type="submit" class="bg-blue-500 hover:bg-blue-700 text-white text-sm font-semibold py-2 px-4 rounded">
                                    Register
                                </button>
                            </div>
                        </form>
                        <form v-else @submit.prevent="confirm" class="form-horizontal w-3/4 mx-auto" method="POST" action="#">
                            <div class="flex flex-col mt-4">
                                <input v-model="confirmForm.email" id="email" type="email" class="flex-grow h-8 px-2 border rounded border-grey-400" name="email" value="" placeholder="Email">
                            </div>
                            <div class="flex flex-col mt-4">
                                <input v-model="confirmForm.code" id="code" type="code" class="flex-grow h-8 px-2 rounded border border-grey-400" name="code" required placeholder="Code">
                            </div>
                            <!-- <div class="flex items-center mt-4">
                                <input type="checkbox" name="remember" id="remember" class="mr-2"> <label for="remember" class="text-sm text-grey-dark">Remember Me</label>
                            </div> -->
                            <div class="flex flex-col mt-8">
                                <button type="submit" class="bg-blue-500 hover:bg-blue-700 text-white text-sm font-semibold py-2 px-4 rounded">
                                    Register
                                </button>
                            </div>
                        </form>
                        <div class="text-center mt-4">
                            <a href="/login" class="no-underline hover:underline text-blue-dark text-xs">
                                Have an account? Login
                            </a>
                        </div>
                    </div>
                </div>
            </div>
            <div class="hidden md:block md:w-1/2 rounded-r-lg" style="background: url('https://images.unsplash.com/photo-1515965885361-f1e0095517ea?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=3300&q=80'); background-size: cover; background-position: center center;"></div>
        </div>
    </div>
  </div>
</template>

<script>
const steps = {
  register: "REGISTER",
  confirm: "CONFIRM"
};
export default {
  mounted() {
    console.log(this.error);
  },
  data: () => ({
    steps: { ...steps },
    step: steps.register,
    registerForm: {
      email: "",
      password: "",
      errors: []
    },
    confirmForm: {
      email: "",
      code: ""
    }
  }),
  methods: {
    async register() {
      try {
        await this.$store.dispatch("auth/register", this.registerForm);
        this.confirmForm.email = this.registerForm.email;
        this.step = this.steps.confirm;
      } catch (error) {
        console.log({ error });
      }
    },
    async confirm() {
      try {
        await this.$store.dispatch(
          "auth/confirmRegistration",
          this.confirmForm
        );
        await this.$store.dispatch("auth/login", this.registerForm);
        this.$router.push("/");
      } catch (error) {
        console.log({ error });
      }
    }
  }
};
</script>

<style>
  
</style>
