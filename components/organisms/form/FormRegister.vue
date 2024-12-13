<template>
  <form
    class="flex flex-col w-full h-auto gap-6 pb-4 text-sm"
    @submit.prevent="register"
  >
    <div class="flex flex-col w-full gap-6 px-4 pt-20 pb-4 bg-sand md:px-6">
      <h3 class="text-lg font-bold">
        Créer un compte
      </h3>
      <div>
        <label for="email">Email</label>
        <InputText
          input-id="email"
          is-required
          placeholder="Email"
          type="email"
          :value.sync="form.email"
        />
      </div>
      <div>
        <label for="lastName">Last Name</label>
        <InputText
          input-id="lastName"
          is-required
          placeholder="LastName"
          :value.sync="form.lastName"
        />
      </div>
      <div>
        <label for="firstName">First Name</label>
        <InputText
          input-id="firstName"
          is-required
          placeholder="FirstName"
          :value.sync="form.firstName"
        />
      </div>
      <div>
        <label for="password">Password</label>
        <InputText
          input-id="password"
          is-required
          placeholder="Password"
          :value.sync="form.password"
          type="password"
        />
      </div>
    </div>
    
    <div class="flex flex-col w-full gap-6 px-4 md:px-6">
      <p
        v-if="errorMessage"
        class="text-red"
      >
        {{ errorMessage }}
      </p>
      <p
        v-if="isRegisteredUser"
        class="text-2xl text-green-900"
      >
       Success, user "{{ userCreated.username }}" created
      </p>
      <BaseButton
        button-type="submit"
        data-testid="form-register-submit"
        :is-loading="isLoading"
      >
        Register
      </BaseButton>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Culpa provident voluptas odit deleniti ducimus voluptatem molestias dicta, aut tenetur doloremque dolorum pariatur tempora necessitatibus blanditiis odio sapiente sit, eligendi consequuntur!</p>
    </div>
  </form>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'FormRegister',
  computed: {
    isRegisteredUser(): boolean {
      return this.userCreated && this.userCreated.username !== '';
    },
  },
  data() {
    return {
      errorMessage: null as String | null,
      form: { // would be typed
        email: '',
        firstName: '',
        lastName: '',
        password: '',
      },
      isLoading: false,
      userCreated: { // would be typed
        username: '',
      },
    };
  },
  methods: {
    async register(): Promise<void> {
      try {
        this.errorMessage = null;
        this.setLoadingState(true);

        // additionnal filtering & form validation in separate method...

        const response = await fetch("https://dummyjson.com/users/add", {
          method: "POST",
          headers: {
            'Content-Type': "application/json",
            'Access-Control-Allow-Credentials': 'true',
          },
          body: JSON.stringify({
            username: this.form.firstName,
            password: this.form.password,
          })
        })
        
        if (!response.ok) {
            throw new Error("Error")
        }
        
        const fmtResponse = await response.json();

        this.userCreated.username = fmtResponse?.username;

      } catch (error) {
        console.log('catching error:', error)
        this.errorMessage = 'Generic error message';
      } finally {
        this.setLoadingState(false);
      }
    },
    setLoadingState(state: boolean): void {
      this.isLoading = state;
    },
  },
});
</script>
