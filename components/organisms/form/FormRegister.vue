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
          :is-disabled="!!currentEmail"
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
      <BaseButton
        button-type="submit"
        data-testid="form-register-submit"
        :is-loading="isLoading"
        is-primary
      >
        Register
      </BaseButton>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Culpa provident voluptas odit deleniti ducimus voluptatem molestias dicta, aut tenetur doloremque dolorum pariatur tempora necessitatibus blanditiis odio sapiente sit, eligendi consequuntur!</p>
    </div>
  </form>
</template>

<script lang="ts">
import Vue, { PropType } from 'vue';


export default Vue.extend({
  name: 'FormRegister',
  props: {
    currentEmail: {
      type: String as PropType<string>,
      default: '',
    },
  },
  data() {
    return {
      errorMessage: null as String | null,
      form: { // would be typed
        email: this.currentEmail || '',
        firstName: '',
        lastName: '',
        password: '',
      },
      isLoading: false,
    };
  },
  methods: {
    async register(): Promise<void> {
      try {
        this.errorMessage = null;
        this.setLoadingState(true);

        // additionnal filtering & form validation...

        await fetch('https://dummyjson.com/auth/login', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({
            username: this.form.firstName,
            password: this.form.password,
            expiresInMins: 30, // optional, defaults to 60
          }),
          credentials: 'include' // Include cookies (e.g., accessToken) in the request
        })
        .then(res => res.json())
        .then(console.log);

        // const user = await this.$services.authService.register(fmtPayload);

        // this.$accessor.user.SET_USER(user); // NOTE: set user but let 'authenticated' set to false.
        // this.handleTracking();

      } catch (error) {
        console.log('catching error:', error)
        this.errorMessage = 'generic error message';
        // this.$errorMonitor.report(error, 'fatal');

        this.setLoadingState(false);
      }
    },
    setLoadingState(state: boolean): void {
      this.isLoading = state;
    },
  },
});
</script>
