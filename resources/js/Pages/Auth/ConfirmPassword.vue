<script setup>
import { Head, useForm } from '@inertiajs/vue3';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';

const form = useForm({
  password: '',
});

const submit = () => {
  form.post(route('password.confirm'), {
    onFinish: () => form.reset(),
  });
};
</script>

<template>
  <GuestLayout>
    <Head title="Confirm Password" />

    <div class="mb-4 text-sm text-gray-600">
      This is a secure area of the application. Please confirm your password before continuing.
    </div>

    <form @submit.prevent="submit">
      <!-- <div>
                <InputLabel for="password" value="Password" />
                <TextInput
                    id="password"
                    type="password"
                    class="mt-1 block w-full"
                    v-model="form.password"
                    required
                    autocomplete="current-password"
                    autofocus
                />
                <InputError class="mt-2" :message="form.errors.password" />
            </div> -->
      <text-input
        v-model="form.password"
        autocomplete="current-password"
        autofocus
        :error-messages="form.errors.email"
        label="Password"
        required
        type="password"
      />

      <div class="flex justify-end mt-4">
        <primary-button
          class="ms-4"
          :disabled="form.processing"
          type="submit"
        >
          Confirm
        </primary-button>
      </div>
    </form>
  </GuestLayout>
</template>
