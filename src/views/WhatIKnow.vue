import CVUK from @

<template>
  <Section id="what-i-know">
    <Abstract2 />

    <v-col cols="12">
      <v-row justify="space-between">
        <Heading cols="auto">
          What I know.
        </Heading>

        <v-col cols="auto">
          <v-btn color="primary" href="/assets/CvUk.pdf">
            <p class="text-black">View cv UK</p>
          </v-btn>

          <footer class="text-center mt-4">
            <v-btn color="primary" href="/assets/CvUS.pdf">
              <p class="text-black">View cv US</p>
            </v-btn>
          </footer>
        </v-col>
      </v-row>
    </v-col>

    <v-col cols="12">
      <v-row justify="space-around">
        <v-col
          id="my-education"
          cols="12"
          md="3"
          tag="section"
        >
          <h3 class="text-h5 font-weight-medium mb-8 text-primary">
            My Education
          </h3>

          <EducationCard
            v-for="(degree, i) in schema.education"
            :key="i"
            :value="degree"
          />
        </v-col>

        <v-col
          id="my-skills"
          cols="12"
          md="6"
          tag="section"
        >
          <h3 class="text-h5 font-weight-medium mb-4 text-primary">
            My Skills
          </h3>

          <p class="skills-description">
            I have included an option to search for skills, that will put a check next to the skill for easy searching.
          </p>

          <!-- SEARCH FORM -->
          <form class="skill-search" @submit.prevent="checkSkill">
            <v-text-field
              v-model="search"
              label="Search skill"
              variant="outlined"
              density="compact"
              hide-details
              @focus="clearSearch"
            />

            <v-btn
              color="primary"
              class="ml-3"
              type="submit"
            >
              Check skill
            </v-btn>
          </form>

          <p v-if="notListed" class="not-listed">
            Not listed
          </p>

          <v-table class="skills-table">
            <tbody>
              <tr
                v-for="row in skillRows"
                :key="row[0]?.name"
              >
                <td v-for="skill in row" :key="skill.name">
                  <div class="skill-item">
                    <span>{{ skill.name }}</span>
                    <span
                      v-if="checkedSkills.has(skill.name)"
                      class="checkmark"
                    >
                      ✔
                    </span>
                  </div>
                </td>
              </tr>
            </tbody>
          </v-table>
        </v-col>
      </v-row>
    </v-col>
  </Section>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import { useAppStore } from '@/stores/app'

const { schema } = useAppStore()

const search = ref('')
const checkedSkills = ref<Set<string>>(new Set())
const notListed = ref(false)

const clearSearch = () => {
  search.value = ''
  notListed.value = false
}

const checkSkill = () => {
  if (!search.value) return

  let found = false

  schema.skills.forEach((skill: { name: string }) => {
    if (skill.name.toLowerCase().includes(search.value.toLowerCase())) {
      checkedSkills.value.add(skill.name)
      found = true
    }
  })

  notListed.value = !found
}

const skillRows = computed(() => {
  const rows = []
  for (let i = 0; i < schema.skills.length; i += 3) {
    rows.push(schema.skills.slice(i, i + 3))
  }
  return rows
})
</script>

<style scoped>
.skills-description {
  margin-bottom: 1.25rem;
}

.skill-search {
  display: flex;
  align-items: center;
  margin-bottom: 0.5rem;
}

.not-listed {
  color: #ff5252;
  font-size: 0.9rem;
  margin-bottom: 1rem;
}

.skills-table {
  border: 1px solid #00bfff;
}

.skills-table td {
  border: 1px solid #00bfff;
  padding: 10px 14px;
  width: 33%;
}

.skill-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-weight: 500;
}

.checkmark {
  color: #2ecc71;
  font-weight: bold;
  font-size: 1.2rem;
}
</style>
