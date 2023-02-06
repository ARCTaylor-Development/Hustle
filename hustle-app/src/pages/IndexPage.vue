<template>
  <q-page class="bg-cyan-4 window-height window-width row justify-center items-center">
    <div class="column">
      <div class="row justify-center items-center">
        <h5 class="text-h2 text-white q-mb-lg">Hustle</h5>
      </div>
      <div class="row q-mb-xl">
        <q-card square bordered class="q-pa-lg shadow-1">
          <q-card-section>
            <q-form class="q-gutter-md">
              <q-input square filled clearable v-model="email" type="email" label="email" />
              <q-input square filled clearable v-model="password" type="password" label="password" />
            </q-form>
          </q-card-section>
          <q-card-actions class="q-px-md">
            <q-btn unelevated @click="loginHandler" color="light-blue-7" size="lg" class="full-width" label="Login" />
          </q-card-actions>
          <q-card-section class="text-center q-pa-none">
            <p class="text-grey-6">Not reigistered? Created an Account</p>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script setup lang="ts">

  import { createBlock, defineComponent, ref, computed, Ref} from 'vue';
import { useRouter } from 'vue-router';
  
  const router = useRouter();

  const validCredentials = {
    "TaidenAylor@example.com": "TestPassword1231",
    "test": "testing"
  }

  const email = ref("");
  const password = ref("");
  const test = "test";

  function loginHandler() {
    console.log("Handling Login Request", email.value, password.value);
    if(!email.value || !password.value) return;
    if(!(email.value in validCredentials) || password.value != validCredentials[email.value as keyof object]) return;
    console.log("Credentials Accepted");
    router.push('/bubbles')
  }

</script>

<style scoped>
  .q-card {
  width: 360px;
}
</style>
