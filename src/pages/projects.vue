<script setup lang="ts">
import ProjectPreview from "@/views/projects/ProjectPreview.vue";

type Project = {title: string, subtitle: string, src: string, languages: string[], technologies: string[], bulletPoints: string[]}

const projects : Project[] = [{
    title: "Daruma",
    subtitle: "A cool eye of Sauron game",
    src: "src/assets/images/projects/daruma.png",
    languages: ["C#"],
    technologies: ["Unity"],
    bulletPoints: ["Implemented a cool hide and seek with sneaking around",
      "Iterated over level design many times to make it look nice"],
  },{
    title: "PaceMaker",
    subtitle: "A cool eye of Sauron game",
    src: "src/assets/images/projects/daruma.png",
    languages: ["Typescript"],
    technologies: ["Vue 3"],
    bulletPoints: ["Implemented a cool hide and seek with sneaking around",
      "Iterated over level design many times to make it look nice"],
  },{
    title: "Experimental Hub",
    subtitle: "A cool eye of Sauron game",
    src: "src/assets/images/projects/daruma.png",
    languages: ["Python", "C++"],
    technologies: [],
    bulletPoints: ["Implemented a cool hide and seek with sneaking around",
      "Iterated over level design many times to make it look nice", "boisssss"],
  },{
    title: "Experimental Hub",
    subtitle: "A cool eye of Sauron game",
    src: "src/assets/images/projects/daruma.png",
    languages: ["Python", "C++"],
    technologies: [],
    bulletPoints: ["Implemented a cool hide and seek with sneaking around",
      "Iterated over level design many times to make it look nice", "boisssss"],
  }]

const languages = projects.flatMap(value => {
  return value.languages
})

const technologies = projects.flatMap(value => {
  return value.technologies
})

const languageSelection = ref([])

const technologySelection = ref([])

function resetLanguageSelection() {
  languageSelection.value = []
}

function resetTechnologySelection() {
  technologySelection.value = []
}

const filters = computed(() => {
  return languageSelection.value.map(id => languages[id]).concat(technologySelection.value.map(id => technologies[id]))
})

watch(technologySelection, () => {
  console.log("hello")
})
</script>

<template>
  <VRow>
    <VCol
      cols="12"
      md="3"
      sm="6"
    >
      <VCard>
        <VCardTitle>
          Language Filter
        </VCardTitle>
        <VCardSubtitle>
          Choose the languages that you want to filter by
        </VCardSubtitle>
        <VCardText>
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
        <VCardActions>
          <VBtn @click="resetLanguageSelection">
            Reset
          </VBtn>
        </VCardActions>
      </VCard>
    </VCol>

    <VCol
      cols="12"
      md="3"
      sm="6"
    >
      <VCard>
        <VCardTitle>
          Technology Filter
        </VCardTitle>
        <VCardSubtitle>
          Choose the technologies that you want to filter by
        </VCardSubtitle>
        <VCardText>
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
          <VBtn @click="resetTechnologySelection">
            Reset
          </VBtn>
        </VCardActions>
      </VCard>
    </VCol>

  </VRow>

  <VRow>
    <!-- Projects -->

    <template v-for="project in projects">

      <VCol
        cols="12"
        lg="3"
        md="4"
        sm="6"
        v-if="filters.length == 0 || filters.some(filter => project.technologies.includes(filter) || project.languages.includes(filter))"
      >
        <ProjectPreview :project="project"/>
      </VCol>

    </template>

  </VRow>
</template>
