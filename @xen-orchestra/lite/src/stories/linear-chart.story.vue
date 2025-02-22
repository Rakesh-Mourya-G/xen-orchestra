<template>
  <ComponentStory
    :params="[
      prop('title').preset('Chart title').widget(),
      prop('subtitle').preset('Here is a subtitle').widget(),
      prop('data')
        .preset(data)
        .required()
        .obj('LinearChartData')
        .help('See doc for typing')
        .widget(),
      prop('value-formatter').type('(value: number) => string'),
      prop('max-value').type('number').widget().default(200),
    ]"
    :presets="presets"
    v-slot="{ properties }"
  >
    <LinearChart v-bind="properties" />
  </ComponentStory>
</template>

<script lang="ts" setup>
import humanFormat from "human-format";
import type { LinearChartData } from "@/types/chart";
import LinearChart from "@/components/charts/LinearChart.vue";
import ComponentStory from "@/components/component-story/ComponentStory.vue";
import { prop } from "@/libs/story/story-param";

const byteFormatter = (value: number) => humanFormat.bytes(value);

let time = 0;
const firstDay = () => (time = 1640995200000);
const nextDay = () => (time += 86400000);

const data: LinearChartData = [
  {
    label: "Foo",
    data: [
      { timestamp: firstDay(), value: 50 },
      { timestamp: nextDay(), value: 20 },
      { timestamp: nextDay(), value: 90 },
      { timestamp: nextDay(), value: 30 },
      { timestamp: nextDay(), value: 70 },
    ],
  },
  {
    label: "Bar",
    data: [
      { timestamp: firstDay(), value: 10 },
      { timestamp: nextDay(), value: 80 },
      { timestamp: nextDay(), value: 30 },
      { timestamp: nextDay(), value: 40 },
      { timestamp: nextDay(), value: 20 },
    ],
  },
];

const presets = {
  "Network bandwidth": {
    props: {
      title: "Network bandwidth",
      subtitle: "Last week",
      "value-formatter": byteFormatter,
      "max-value": 500000000,
      data: [
        {
          label: "Download",
          data: [
            {
              timestamp: firstDay(),
              value: 4986790,
            },
            {
              timestamp: nextDay(),
              value: 354312074,
            },
            {
              timestamp: nextDay(),
              value: 379858800,
            },
            {
              timestamp: nextDay(),
              value: 319522087,
            },
            {
              timestamp: nextDay(),
              value: 344568079,
            },
            {
              timestamp: nextDay(),
              value: 46295651,
            },
            {
              timestamp: nextDay(),
              value: 344130914,
            },
          ],
        },
        {
          label: "Upload",
          data: [
            {
              timestamp: firstDay(),
              value: 102528411,
            },
            {
              timestamp: nextDay(),
              value: 10682534,
            },
            {
              timestamp: nextDay(),
              value: 10421188,
            },
            {
              timestamp: nextDay(),
              value: 102156882,
            },
            {
              timestamp: nextDay(),
              value: 102028168,
            },
            {
              timestamp: nextDay(),
              value: 102733601,
            },
            {
              timestamp: nextDay(),
              value: 102523226,
            },
          ],
        },
      ],
    },
  },
};
</script>

<style lang="postcss" scoped></style>
