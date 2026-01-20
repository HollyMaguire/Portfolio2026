<template>
  <Section id="who-i-am">
    <Abstract1 />

    <Heading>Who I am.</Heading>

    <v-col
      cols="12"
      md="7"
    >
      <v-row justify="space-between">
        <v-col
          cols="12"
          md="7"
        >
          <Text class="mb-0">
            <p>I am a Software Engineer with full-stack skills, who specializes in front-end engineering/development.
 I enjoy making
    responsive, accessible UI and have professional experience with: React, Angular,
    Vue, JavaScript, TypeScript, Elm, HTML5, CSS/SCSS, along with UI/UX design collaboration and
    accessibility focused development.
    I bring a versatile background from prior full stack roles, with experience across Python, Ruby,
    Java, C# and Fortran.</p>
            <div>
                <p class="text-uppercase text-primary font-weight-medium" >I am authorized to work in the UK and the US</p>
            </div>
          </Text>
        </v-col>

        <v-col
          cols="12"
          md="4"
        >
          <v-row align="center">
            <v-col
              class="text-uppercase text-primary font-weight-medium"
              cols="6"
            >
              <div
                class="mb-3"
              >Email</div>
              <div
                class="mb-3"
              >Phone</div>
        
            </v-col>
            <v-col
              class="text-no-wrap"
              cols="6"
            >
              <div
                class="mb-3"
              >Hollygracemaguire@gmail.com</div>
              <div
                class="mb-3"
              >{{ schema.basics.phone }}</div>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-col>
  </Section>
</template>

<script setup lang="ts">
  import { useAppStore } from '@/stores/app'

  const { schema } = useAppStore()
</script>

<style lang="sass">
  .v-expansion-panels > li
    border-top: 1px solid rgba(#fff, .12) !important
</style>
