<script setup>
import { Head, Link, useForm } from '@inertiajs/vue3';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';

const form = useForm({
  name: '',
  email: '',
  password: '',
  password_confirmation: '',
});

const submit = () => {
  form.post(route('register'), {
    onFinish: () => form.reset('password', 'password_confirmation'),
  });
};
</script>

<template>
  <GuestLayout>
    <Head title="Register" />

    <form @submit.prevent="submit">
      <!-- <div>
                <InputLabel for="name" value="Name" />

                <TextInput
                    id="name"
                    type="text"
                    class="mt-1 block w-full"
                    v-model="form.name"
                    required
                    autofocus
                    autocomplete="name"
                />

                <InputError class="mt-2" :message="form.errors.name" />
            </div> -->

      <text-input
        v-model="form.name"
        autocomplete="name"
        autofocus
        class="mt-2"
        :error-messages="form.errors.name"
        label="Name"
        required
        type="text"
      />

      <!-- <div class="mt-4">
                <InputLabel for="email" value="Email" />

                <TextInput
                    id="email"
                    type="email"
                    class="mt-1 block w-full"
                    v-model="form.email"
                    required
                    autocomplete="username"
                />

                <InputError class="mt-2" :message="form.errors.email" />
            </div> -->

      <text-input
        v-model="form.email"
        autocomplete="username"
        autofocus
        class="mt-4"
        :error-messages="form.errors.email"
        label="Email"
        required
        type="email"
      />

      <!-- <div class="mt-4">
                <InputLabel for="password" value="Password" />

                <TextInput
                    id="password"
                    type="password"
                    class="mt-1 block w-full"
                    v-model="form.password"
                    required
                    autocomplete="new-password"
                />

                <InputError class="mt-2" :message="form.errors.password" />
            </div> -->

      <text-input
        v-model="form.password"
        autocomplete="new-password"
        class="mt-4"
        :error-messages="form.errors.password"
        label="Password"
        required
        type="password"
      />

      <!-- <div class="mt-4">
                <InputLabel for="password_confirmation" value="Confirm Password" />

                <TextInput
                    id="password_confirmation"
                    type="password"
                    class="mt-1 block w-full"
                    v-model="form.password_confirmation"
                    required
                    autocomplete="new-password"
                />

                <InputError class="mt-2" :message="form.errors.password_confirmation" />
            </div> -->

      <text-input
        v-model="form.password_confirmation"
        autocomplete="new-password"
        class="mt-4"
        :error-messages="form.errors.password_confirmation"
        label="Confirm Password"
        required
        type="password"
      />

      <div class="flex items-center justify-end mt-4">
        <Link
          class="underline text-sm text-gray-600 hover:text-gray-900 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
          :href="route('login')"
        >
          Already registered?
        </Link>

        <primary-button
          class="ms-4"
          :disabled="form.processing"
          type="submit"
        >
          Register
        </primary-button>
      </div>
    </form>
  </GuestLayout>
</template>
