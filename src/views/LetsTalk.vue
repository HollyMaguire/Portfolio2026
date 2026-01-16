<template>
  <Section id="lets-talk">
    <Heading>Let's talk.</Heading>

    <v-col
      class="mb-4 pr-md-5"
      cols="12"
      md="5"
    >
    </v-col>

    <v-col
      class="text-left"
      cols="12"
      md="4"
    >
      <Subheading class="text-uppercase">
        Social Contacts
      </Subheading>

      <SocialContacts />

      <v-list
        class="bg-transparent"
        lines="two"
      >
        <v-list-item>
          <template #prepend>
            <v-icon
              color="primary"
              icon="mdi-email"
              size="48"
            />
          </template>
          <v-list-item-title class="text-primary">
            Email
          </v-list-item-title>
          <v-list-item-subtitle>{{ schema.basics.email }}</v-list-item-subtitle>
        </v-list-item>
        <v-list-item>
          <template #prepend>
            <v-icon
              color="primary"
              icon="mdi-phone"
              size="48"
            />
          </template>
          <v-list-item-title class="text-primary">
            Phone
          </v-list-item-title>
          <v-list-item-subtitle>{{ schema.basics.phone }}</v-list-item-subtitle>
        </v-list-item>
      </v-list>
    </v-col>
    <!-- <v-img
      max-height="100%"
      max-width="30vw"
      src="/assets/john-alt.png"
      style="bottom: 0; right: 0; position: absolute; display: flex; align-items: end;"
      width="100%"
    /> -->
  </Section>
</template>

<script setup lang="ts">
  import { useAppStore } from '@/stores/app'
  const { schema } = useAppStore()
</script>
