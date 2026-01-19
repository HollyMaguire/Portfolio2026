<template>
  <v-sheet
    class="mb-5"
    color="transparent"
  >
    <v-row class="mx-0">
      <v-sheet
        class="mr-3"
        color="primary"
        height="100"
        width="1"
        tile
      />

      <v-col>
        <div
          class="mb-3"
        >{{ value.institution }}</div>

        <div class="text-right">
          <span
            class="text-h6 text-primary"
          >{{ value.studyType + value.area }}</span>

          <footer>
            <div
              v-for="(course, i) in value.courses"
              :key="i"
            >{{ course }}</div>
          </footer>
        </div>
      </v-col>
    </v-row>
  </v-sheet>
</template>

<script setup lang="ts">
  interface Props {
    value : {
      institution: string,
      area: string,
      studyType: string,
      courses: Array<any>,
    }
  }

  const props = withDefaults(defineProps<Props>(), {
    value: () => ({
      institution: '',
      area: '',
      studyType: '',
      startDate: '',
      endDate: '',
      gpa: '',
      courses: [],
    }),
  })

</script>
