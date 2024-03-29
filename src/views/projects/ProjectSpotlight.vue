<script setup lang="ts">
import VueApexCharts from 'vue3-apexcharts'
import { useDisplay, useTheme } from 'vuetify'

import { hexToRgb } from '@layouts/utils'

interface Project { title: string; subtitle: string; src: string; languages: string[]; technologies: string[]; bulletPoints: string[] }

const props = defineProps<{ project: Project }>()

const vuetifyTheme = useTheme()
const display = useDisplay()

const moreList = [
  { title: 'Share', value: 'Share' },
  { title: 'Refresh', value: 'Refresh' },
  { title: 'Update', value: 'Update' },
]

const series = [
  { name: `${new Date().getFullYear() - 1}`, data: [18, 7, 15, 29, 18, 12, 9] },
  { name: `${new Date().getFullYear() - 2}`, data: [-13, -18, -9, -14, -5, -17, -15] },
]

const chartOptions = computed(() => {
  const currentTheme = vuetifyTheme.current.value.colors
  const variableTheme = vuetifyTheme.current.value.variables

  const disabledTextColor = `rgba(${hexToRgb(String(currentTheme['on-surface']))},${variableTheme['disabled-opacity']})`
  const primaryTextColor = `rgba(${hexToRgb(String(currentTheme['on-surface']))},${variableTheme['high-emphasis-opacity']})`
  const borderColor = `rgba(${hexToRgb(String(variableTheme['border-color']))},${variableTheme['border-opacity']})`

  return {
    bar: {
      chart: {
        stacked: true,
        parentHeightOffset: 0,
        toolbar: { show: false },
      },
      dataLabels: { enabled: false },
      stroke: {
        width: 6,
        lineCap: 'round',
        colors: [currentTheme.surface],
      },
      colors: [`rgba(${hexToRgb(String(currentTheme.primary))}, 1)`, `rgba(${hexToRgb(String(currentTheme.info))}, 1)`],
      legend: {
        offsetX: -10,
        position: 'top',
        fontSize: '14px',
        horizontalAlign: 'left',
        fontFamily: 'Public Sans',
        labels: {
          colors: currentTheme.secondary,
        },
        itemMargin: {
          vertical: 4,
          horizontal: 10,
        },
        markers: {
          width: 8,
          height: 8,
          radius: 10,
          offsetX: -4,
        },
      },
      states: {
        hover: {
          filter: { type: 'none' },
        },
        active: {
          filter: { type: 'none' },
        },
      },
      grid: {
        borderColor,
        padding: {
          bottom: 5,
        },
      },
      plotOptions: {
        bar: {
          borderRadius: 10,
          columnWidth: '30%',
          endingShape: 'rounded',
          startingShape: 'rounded',
        },
      },
      xaxis: {
        axisTicks: { show: false },
        crosshairs: { opacity: 0 },
        axisBorder: { show: false },
        categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul'],
        labels: {
          style: {
            fontSize: '14px',
            colors: disabledTextColor,
            fontFamily: 'Public Sans',
          },
        },
      },
      yaxis: {
        labels: {
          style: {
            fontSize: '14px',
            colors: disabledTextColor,
            fontFamily: 'Public Sans',
          },
        },
      },
      responsive: [
        {
          breakpoint: display.thresholds.value.xl,
          options: {
            plotOptions: {
              bar: { columnWidth: '43%' },
            },
          },
        },
        {
          breakpoint: display.thresholds.value.lg,
          options: {
            plotOptions: {
              bar: { columnWidth: '50%' },
            },
          },
        },
        {
          breakpoint: display.thresholds.value.md,
          options: {
            plotOptions: {
              bar: { columnWidth: '42%' },
            },
          },
        },
        {
          breakpoint: display.thresholds.value.sm,
          options: {
            plotOptions: {
              bar: { columnWidth: '45%' },
            },
          },
        },
      ],
    },
    radial: {
      chart: {
        sparkline: { enabled: true },
      },
      labels: ['Growth'],
      stroke: { dashArray: 5 },
      colors: [`rgba(${hexToRgb(String(currentTheme.primary))}, 1)`],
      states: {
        hover: {
          filter: { type: 'none' },
        },
        active: {
          filter: { type: 'none' },
        },
      },
      fill: {
        type: 'gradient',
        gradient: {
          shade: 'dark',
          opacityTo: 0.6,
          opacityFrom: 1,
          shadeIntensity: 0.5,
          stops: [30, 70, 100],
          inverseColors: false,
          gradientToColors: [currentTheme.primary],
        },
      },
      plotOptions: {
        radialBar: {
          endAngle: 150,
          startAngle: -140,
          hollow: { size: '55%' },
          track: { background: 'transparent' },
          dataLabels: {
            name: {
              offsetY: 25,
              fontWeight: 600,
              fontSize: '16px',
              color: currentTheme.secondary,
              fontFamily: 'Public Sans',
            },
            value: {
              offsetY: -15,
              fontWeight: 500,
              fontSize: '24px',
              color: primaryTextColor,
              fontFamily: 'Public Sans',
            },
          },
        },
      },
      responsive: [
        {
          breakpoint: 900,
          options: {
            chart: { height: 200 },
          },
        },
        {
          breakpoint: 735,
          options: {
            chart: { height: 200 },
          },
        },
        {
          breakpoint: 660,
          options: {
            chart: { height: 200 },
          },
        },
        {
          breakpoint: 600,
          options: {
            chart: { height: 280 },
          },
        },
      ],
    },
  }
})

const balanceData = [
  { icon: 'bx-dollar', amount: '$32.5k', year: '2023', color: 'primary' },
  { icon: 'bx-wallet', amount: '$41.2k', year: '2022', color: 'info' },
]
</script>

<template>
  <VCard>
    <VRow no-gutters>
      <VCol
        cols="12"
        sm="8"
        xl="7"
        :class="$vuetify.display.smAndUp ? 'border-e' : 'border-b'"
      >
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
            <VChip v-for="language in project.languages">
              {{ language }}
            </VChip>

            <VChip v-for="technology in project.technologies">
              {{ technology }}
            </VChip>
          </VChipGroup>
        </VCardText>
      </VCol>

      <VCol
        cols="12"
        sm="5"
        xl="5"
      >
        <VCardText>
          <VList class="card-list mt-7">
            <VListItem v-for="bulletPoint in project.bulletPoints">
              <template #prepend>
                <VAvatar
                  rounded
                  variant="tonal"
                  color="info"
                >
                  <VIcon icon="bx-right-arrow-circle" />
                </VAvatar>
              </template>

              {{ bulletPoint }}
            </VListItem>
          </VList>
        </VCardText>
      </VCol>
    </VRow>
  </VCard>
</template>

<style lang="scss">
#bar-chart .apexcharts-series[rel="2"] {
  transform: translateY(-10px);
}
</style>
