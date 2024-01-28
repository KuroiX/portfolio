<script setup lang="ts">
import ProjectPreview from '@/views/projects/ProjectPreview.vue'
import ProjectSpotlight from "@/views/projects/ProjectSpotlight.vue";

interface Project { title: string; subtitle: string; src: string; languages: string[]; technologies: string[]; bulletPoints: string[] }

const projects: Project[] = [{
  title: 'shattered',
  subtitle: 'See 3D with autostereograms (magic eye)!',
  src: 'src/assets/images/projects/shattered.png',
  languages: ['C#', 'HLSL'],
  technologies: ['Unity'],
  bulletPoints: ['Developed a highly technical shader utilizing multiple sub-steps in the graphics pipeline',
    'Implemented an innovative algorithm to create an autostereogram of the entire scene, enabling the perception of 3D images on a standard screen',
    'Details + Windows Build: https://kuroix.itch.io/shattered'],
}, {
  title: 'janken-pose',
  subtitle: 'An arcade-style rock-paper-scissors game using full-body poses!',
  src: 'src/assets/images/projects/daruma.png',
  languages: ['C#'],
  technologies: ['Unity', 'Kinect'],
  bulletPoints: ['Developed an immersive mixed-reality game utilizing Kinect technology',
    'Implemented a sophisticated algorithm leveraging linear algebra to recognize and capture player poses',
    'Calculated joint angles and directions, ensuring accurate and responsive pose recognition during gameplay'],
}, {
  title: 'FastState',
  subtitle: 'A high-performance implementation of state charts',
  src: 'src/assets/images/projects/daruma.png',
  languages: ['C#'],
  technologies: [],
  bulletPoints: ['Utilized data-oriented programming principles inspired by Unity DOTS (Data-Oriented Technology Stack) and the Entity Component System (ECS)',
    'Implemented a streamlined approach by simplifying states to bitmasks',
    'Leveraged native processor operations for bit-wise comparisons, enhancing computational efficiency'],
},]

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
      sm="4"
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
    <!--
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
        :lg="i === 0 ? 8 : 3"
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
