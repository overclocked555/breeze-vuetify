<script setup>
import { Link } from '@inertiajs/vue3';
import { useDisplay } from 'vuetify';
import ApplicationLogo from '@/Components/ApplicationLogo.vue';

const { smAndUp } = useDisplay();
</script>

<template>
  <!-- <div class="min-h-screen flex flex-col sm:justify-center items-center pt-6 sm:pt-0 bg-gray-100"> -->
  <v-app>
    <v-main>
      <v-container
        class="fill-height flex-column justify-center align-center"
        fluid
      >
        <div>
          <Link href="/">
            <ApplicationLogo class="w-20 h-20 fill-current text-gray-500" />
          </Link>
        </div>
        <v-card
          class="mt-6 py-2 align-self-stretch align-self-sm-auto"
          :width="smAndUp ? 500 : undefined"
        >
          <v-card-item>
            <!-- <div class="w-full sm:max-w-md mt-6 px-6 py-4 bg-white shadow-md overflow-hidden sm:rounded-lg"> -->
            <slot />
            <!-- </div> -->
          </v-card-item>
        </v-card>
      </v-container>
    </v-main>
  </v-app>
  <!-- </div> -->
</template>
