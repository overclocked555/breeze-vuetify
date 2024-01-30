<script setup>
import { useForm } from '@inertiajs/vue3';
import { ref } from 'vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';

const passwordInput = ref(null);
const currentPasswordInput = ref(null);

const form = useForm({
  current_password: '',
  password: '',
  password_confirmation: '',
});

const submit = () => {
  form.put(route('password.update'), {
    preserveScroll: true,
    onSuccess: () => form.reset(),
    onError: () => {
      if (form.errors.password) {
        form.reset('password', 'password_confirmation');
        passwordInput.value.focus();
      }
      if (form.errors.current_password) {
        form.reset('current_password');
        currentPasswordInput.value.focus();
      }
    },
  });
};
</script>

<template>
  <section>
    <header>
      <h2 class="text-lg font-medium text-gray-900">
        Update Password
      </h2>

      <p class="mt-1 text-sm text-gray-600">
        Ensure your account is using a long, random password to stay secure.
      </p>
    </header>

    <form
      class="mt-6 space-y-6"
      @submit.prevent="submit"
    >
      <!-- <div>
                <InputLabel for="current_password" value="Current Password" />

                <TextInput id="current_password" ref="currentPasswordInput" v-model="form.current_password" type="password"
                    class="mt-1 block w-full" autocomplete="current-password" />

                <InputError :message="form.errors.current_password" class="mt-2" />
            </div> -->

      <text-input
        ref="currentPasswordInput"
        v-model="form.current_password"
        autocomplete="current-password"
        :error-messages="form.errors.current_password"
        label="Current Password"
        required
        type="password"
      />

      <!-- <div>
                <InputLabel for="password" value="New Password" />

                <TextInput id="password" ref="passwordInput" v-model="form.password" type="password"
                    class="mt-1 block w-full" autocomplete="new-password" />

                <InputError :message="form.errors.password" class="mt-2" />
            </div> -->

      <text-input
        ref="passwordInput"
        v-model="form.password"
        autocomplete="new-password"
        :error-messages="form.errors.password"
        label="New Password"
        required
        type="password"
      />

      <!-- <div>
                <InputLabel for="password_confirmation" value="Confirm Password" />

                <TextInput id="password_confirmation" v-model="form.password_confirmation" type="password"
                    class="mt-1 block w-full" autocomplete="new-password" />

                <InputError :message="form.errors.password_confirmation" class="mt-2" />
            </div> -->

      <text-input
        v-model="form.password_confirmation"
        autocomplete="new-password"
        :error-messages="form.errors.password_confirmation"
        label="Confirm Password"
        required
        type="password"
      />

      <div class="flex items-center gap-4">
        <primary-button
          :disabled="form.processing"
          type="submit"
        >
          Save
        </primary-button>

        <Transition
          enter-active-class="transition ease-in-out"
          enter-from-class="opacity-0"
          leave-active-class="transition ease-in-out"
          leave-to-class="opacity-0"
        >
          <p
            v-if="form.recentlySuccessful"
            class="text-sm text-gray-600"
          >
            Saved.
          </p>
        </Transition>
      </div>
    </form>
  </section>
</template>
