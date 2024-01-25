<script setup lang="ts">
import { useTheme } from 'vuetify'

type Project = {title: string, subtitle: string, src: string, languages: string[], technologies: string[], bulletPoints: string[]}

const props = defineProps<{project: Project}>()

const vuetifyTheme = useTheme()

const orders = [
  {
    amount: '82.5k',
    title: 'Electronic',
    avatarColor: 'primary',
    subtitle: 'Mobile, Earbuds, TV',
    avatarIcon: 'bx-mobile-alt',
  },
  {
    amount: '23.8k',
    title: 'Fashion',
    avatarColor: 'success',
    subtitle: 'Tshirt, Jeans, Shoes',
    avatarIcon: 'bx-closet',
  },
  {
    amount: 849,
    title: 'Decor',
    avatarColor: 'info',
    subtitle: 'Fine Art, Dining',
    avatarIcon: 'bx-home',
  },
  {
    amount: 99,
    title: 'Sports',
    avatarColor: 'secondary',
    subtitle: 'Football, Cricket Kit',
    avatarIcon: 'bx-football',
  },
]

const moreList = [
  { title: 'Share', value: 'Share' },
  { title: 'Refresh', value: 'Refresh' },
  { title: 'Update', value: 'Update' },
]
</script>

<template>
  <VCard>
    <VImg
      cover
      :src="project.src"
    >
      <!--
      <VCardTitle class="text-primary">
        Daruma
      </VCardTitle>
      <VCardSubtitle>
        A cool game with the eye of Sauron!
      </VCardSubtitle>
      -->
    </VImg>

    <VCardItem class="pb-3">
      <VCardTitle class="mb-1">
        {{ project.title }}
      </VCardTitle>
      <VCardSubtitle>{{ project.subtitle }}</VCardSubtitle>

      <template #append>
        <div class="me-n3 mt-n8">
          <MoreBtn :menu-list="moreList" />
        </div>
      </template>
    </VCardItem>

    <VCardText>
      <VChipGroup>
        <VChip
          v-for="language in project.languages"
        >
          {{ language }}
        </VChip>

        <VChip
          v-for="technology in project.technologies"
        >
          {{ technology }}
        </VChip>
      </VChipGroup>

      <VList class="card-list mt-7">
        <VListItem
          v-for="bulletPoint in project.bulletPoints"
        >
          <template #prepend>
            <VAvatar
              rounded
              variant="tonal"
              color="primary"
            >
              <VIcon icon="bx-right-arrow-circle" />
            </VAvatar>
          </template>

          {{ bulletPoint }}
        </VListItem>

      </VList>
    </VCardText>
  </VCard>
</template>

<style lang="scss" scoped>
.card-list {
  --v-card-list-gap: 21px;
}
</style>
