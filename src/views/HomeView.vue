<template>
  <v-container fluid class="primary fill-height">
    <v-row>
      <v-col>
        <v-card width="400" class="mx-auto mt-5">
          <v-card-title>
            <h2 class="display-1">Login</h2>
          </v-card-title>
          <v-card-text>
            <v-form>
              <v-text-field label="Email" v-model="v$.userEmail.$model" />
              <div v-if="v$.userEmail.$error" class="text-red">
                Email is not correct
              </div>
              <v-text-field
                type="password"
                label="Password"
                v-model="v$.userPassword.$model"
              />
              <div v-if="v$.userPassword.$error" class="text-red">
                Password must be longer than 6 characters
              </div>
            </v-form>
          </v-card-text>
          <v-divider></v-divider>
          <v-card-actions>
            <v-btn color="info" @click="submitForm">Login</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref, computed } from "vue";
import { useRouter } from "vue-router";
import { useVuelidate } from "@vuelidate/core";
import { required, email, minLength } from "@vuelidate/validators";

const router = useRouter();

const userEmail = ref("");
const userPassword = ref("");

const rules = computed(() => ({
  userEmail: {
    required,
    email,
  },
  userPassword: {
    required,
    minLength: minLength(6),
  },
}));
const v$ = useVuelidate(rules, { userEmail, userPassword });

const submitForm = async () => {
  v$.value.$touch();
  if (v$.value.$error) return;

  router.push("/game");
};
</script>
