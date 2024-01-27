<script setup lang="ts">
import ProjectPreview from '@/views/projects/ProjectPreview.vue'
import ProjectSpotlight from "@/views/projects/ProjectSpotlight.vue";

interface Project { title: string; subtitle: string; src: string; languages: string[]; technologies: string[]; bulletPoints: string[] }

const projects: Project[] = [{
  title: 'Daruma',
  subtitle: 'A cool eye of Sauron game',
  src: 'src/assets/images/projects/daruma.png',
  languages: ['C#'],
  technologies: ['Unity'],
  bulletPoints: ['Implemented a cool hide and seek with sneaking around',
    'Iterated over level design many times to make it look nice'],
}, {
  title: 'PaceMaker',
  subtitle: 'A cool eye of Sauron game',
  src: 'src/assets/images/projects/daruma.png',
  languages: ['Typescript'],
  technologies: ['Vue 3'],
  bulletPoints: ['Implemented a cool hide and seek with sneaking around',
    'Iterated over level design many times to make it look nice'],
}, {
  title: 'Experimental Hub',
  subtitle: 'A cool eye of Sauron game',
  src: 'src/assets/images/projects/daruma.png',
  languages: ['Python', 'C++'],
  technologies: [],
  bulletPoints: ['Implemented a cool hide and seek with sneaking around',
    'Iterated over level design many times to make it look nice',
    'boisssss'],
}, {
  title: 'Experimental Hub',
  subtitle: 'A cool eye of Sauron game',
  src: 'src/assets/images/projects/daruma.png',
  languages: ['Python', 'C++'],
  technologies: [],
  bulletPoints: ['Implemented a cool hide and seek with sneaking around',
    'Iterated over level design many times to make it look nice',
    'boisssss'],
}]

const languages = [...new Set(projects.flatMap(value => {
  return value.languages
}))]

const technologies = [...new Set(projects.flatMap(value => {
  return value.technologies
}))]

const languageSelection = ref([])

const technologySelection = ref([])

const filters = computed(() => {
  return languageSelection.value.map(id => languages[id]).concat(technologySelection.value.map(id => technologies[id]))
})

const selection = computed(() =>
  projects.filter(project => filters.value.length === 0 || filters.value.every(filter => project.technologies.includes(filter) || project.languages.includes(filter)))
)

function resetSelection() {
  resetLanguageSelection()
  resetTechnologySelection()
}

function resetLanguageSelection() {
  languageSelection.value = []
}

function resetTechnologySelection() {
  technologySelection.value = []
}

</script>

<template>
  <VRow>
    <VCol
      cols="12"
      md="4"
      sm="6"
      order="1"
    >

      <VCard variant="outlined" >
        <VCardTitle>
          Filters
        </VCardTitle>
        <VCardSubtitle>
          You can filter the projects by various categories.
        </VCardSubtitle>
        <VCardText>
          Languages
          <VChipGroup
            v-model="languageSelection"
            selected-class="text-primary"
            multiple
            filter
          >
            <VChip v-for="language in languages">
              {{ language }}
            </VChip>
          </VChipGroup>
        </VCardText>
        <VCardText>
          Technologies
          <VChipGroup
            v-model="technologySelection"
            selected-class="text-primary"
            multiple
            filter
          >
            <VChip v-for="technology in technologies">
              {{ technology }}
            </VChip>
          </VChipGroup>
        </VCardText>
        <VCardActions>
          <VBtn @click="resetSelection">
            Reset
          </VBtn>
        </VCardActions>
      </VCard>
    </VCol>
    <VCol
      cols="12"
      md="2"
      sm="6"
      order="1"
    >
      <VCard>
        Hello
      </VCard>
    </VCol>
    <!--
    <VCol
      cols="12"
      order="1"
    >
      <VRow>
        <VCol
          cols="12"
          md="4"
          sm="6"
          order="1"
        >

          <VCard variant="outlined" >
            <VCardTitle>
              Filters
            </VCardTitle>
            <VCardSubtitle>
              You can filter the projects by various categories.
            </VCardSubtitle>
            <VCardText>
              Languages
              <VChipGroup
                v-model="languageSelection"
                selected-class="text-primary"
                multiple
                filter
              >
                <VChip v-for="language in languages">
                  {{ language }}
                </VChip>
              </VChipGroup>
            </VCardText>
            <VCardText>
              Technologies
              <VChipGroup
                v-model="technologySelection"
                selected-class="text-primary"
                multiple
                filter
              >
                <VChip v-for="technology in technologies">
                  {{ technology }}
                </VChip>
              </VChipGroup>
            </VCardText>
            <VCardActions>
              <VBtn @click="resetSelection">
                Reset
              </VBtn>
            </VCardActions>
          </VCard>
        </VCol>
        <VCol
          cols="12"
          md="2"
          sm="6"
          order="1"
        >
          <VCard>
            Hello
          </VCard>
        </VCol>
      </VRow>
      <VRow>
        <VCol
          cols="12"
          md="4"
          sm="6"
          order="1"
        >

          <VCard variant="outlined" >
            <VCardTitle>
              Filters
            </VCardTitle>
            <VCardSubtitle>
              You can filter the projects by various categories.
            </VCardSubtitle>
            <VCardText>
              Languages
              <VChipGroup
                v-model="languageSelection"
                selected-class="text-primary"
                multiple
                filter
              >
                <VChip v-for="language in languages">
                  {{ language }}
                </VChip>
              </VChipGroup>
            </VCardText>
            <VCardText>
              Technologies
              <VChipGroup
                v-model="technologySelection"
                selected-class="text-primary"
                multiple
                filter
              >
                <VChip v-for="technology in technologies">
                  {{ technology }}
                </VChip>
              </VChipGroup>
            </VCardText>
            <VCardActions>
              <VBtn @click="resetSelection">
                Reset
              </VBtn>
            </VCardActions>
          </VCard>
        </VCol>
        <VCol
          cols="12"
          md="2"
          sm="6"
          order="1"
        >
          <VCard>
            Hello
          </VCard>
        </VCol>
      </VRow>
    </VCol>
    -->

    <!-- Projects -->
    <VCol
      v-if="selection.length === 0"
      cols="12"
      lg="6"
      md="4"
      sm="6"
      order="0"
    >
      <VCard>
        <VCardTitle>
          No project found!
        </VCardTitle>
      </VCard>
    </VCol>

    <template v-for="(project, i) in selection">
      <VCol
        cols="12"
        :lg="i === 0 ? 6 : 3"
        md="4"
        sm="6"
        :order="i === 0 ? '0' : '2'"
      >
        <ProjectSpotlight v-if="i === 0" :project="project"/>
        <ProjectPreview v-else :project="project" />
      </VCol>
    </template>
  </VRow>
</template>
