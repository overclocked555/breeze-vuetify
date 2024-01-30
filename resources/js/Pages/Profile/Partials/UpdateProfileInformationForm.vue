<script setup>
import { Link, useForm, usePage } from '@inertiajs/vue3';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';

defineProps({
  mustVerifyEmail: {
    type: Boolean,
  },
  status: {
    type: String,
  },
});

const { user } = usePage().props.auth;

const form = useForm({
  name: user.name,
  email: user.email,
});

const submit = () => {
  form.patch(route('profile.update'));
};
</script>

<template>
  <section>
    <header>
      <h2 class="text-lg font-medium text-gray-900">
        Profile Information
      </h2>

      <p class="mt-1 text-sm text-gray-600">
        Update your account's profile information and email address.
      </p>
    </header>

    <form
      class="mt-6 space-y-6"
      @submit.prevent="submit"
    >
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
        :error-messages="form.errors.name"
        label="Name"
        required
        type="text"
      />

      <!-- <div>
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
        class="mt-4"
        :error-messages="form.errors.email"
        label="Email"
        required
        type="email"
      />

      <div v-if="mustVerifyEmail && user.email_verified_at === null">
        <p class="text-sm mt-2 text-gray-800">
          Your email address is unverified.
          <Link
            as="button"
            class="underline text-sm text-gray-600 hover:text-gray-900 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            :href="route('verification.send')"
            method="post"
          >
            Click here to re-send the verification email.
          </Link>
        </p>

        <div
          v-show="status === 'verification-link-sent'"
          class="mt-2 font-medium text-sm text-green-600"
        >
          A new verification link has been sent to your email address.
        </div>
      </div>

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
