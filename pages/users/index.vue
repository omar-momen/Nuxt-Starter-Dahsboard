<template>
  <BaseTable
    :table_title="$t(`CRUDS.tasks.title`)"
    :columns="columns"
    :form="form"
    :filters="filters"
    endpoint="tasks"
  >
    <!-- Pass 'expandable' prop to 'BaseTable' and implement your expanded section here as wanted -->
    <template #expand="{ row }">
      {{ row.name }}
    </template>
  </BaseTable>
</template>

<script setup lang="ts">
definePageMeta({
  title: "Posts",
  requireAuth: true,
});

// =====> Data
const { GENDERS_OPTIONS } = useConstants();

// =====> Locals
const { t } = useI18n();

// =====> Columns
const columns = [
  {
    key: "id",
    label: "#",
    sortable: true,
  },
  {
    key: "image",
    label: t("labels.image"),
  },
  {
    key: "name",
    label: t("labels.name"),
    sortable: true,
  },
  {
    key: "description",
    label: t("labels.description"),
  },
  {
    key: "created_at",
    label: t("labels.created_at"),
  },
  {
    key: "updated_at",
    label: t("labels.updated_at"),
  },
  {
    key: "lesson_id",
    label: t("labels.lesson"),
  },
  {
    key: "tickets",
    label: t("labels.tickets"),
  },
];

// =====> Form Inputs
const form = [
  {
    key: "image",
    label: t("labels.image"),
    placeholder: `${t("labels.upload")} ${t("labels.image")}`,
    type: "file-image",
    required: true,
  },
  {
    key: "name",
    label: t("labels.name"),
    placeholder: `${t("labels.enter")} ${t("labels.name")}`,
    type: "text",
    required: true,
  },
  {
    key: "description",
    label: t("labels.description"),
    placeholder: `${t("labels.enter")} ${t("labels.description")}`,
    type: "textarea",
    required: true,
  },
  {
    key: "lesson_id",
    label: t("labels.lesson"),
    placeholder: `${t("labels.choose")} ${t("labels.lesson")}`,
    type: "select",
    getEndpoint: "lessons",
    required: true,
  },
  {
    key: "tickets",
    label: t("labels.tickets"),
    placeholder: `${t("labels.choose")} ${t("labels.tickets")}`,
    type: "select",
    getEndpoint: "tickets",
    multiple: true,
    required: true,
  },
  {
    key: "gender",
    label: t("labels.gender"),
    placeholder: `${t("labels.choose")} ${t("labels.gender")}`,
    options: GENDERS_OPTIONS,
    type: "select",
    required: true,
  },
  {
    key: "is_active",
    label: t("labels.is_active"),
    type: "switch",
  },
];

// =====> Filters
const filters = [
  {
    key: "name",
    label: t("labels.name"),
    placeholder: `${t("labels.search_with")} ${t("labels.name")} ...`,
    type: "search",
  },
  {
    key: "lesson_id",
    label: t("labels.lesson"),
    placeholder: `${t("labels.choose")} ${t("labels.lesson")}`,
    type: "select",
    getEndpoint: "lessons",
  },
  {
    key: "tickets",
    label: t("labels.tickets"),
    placeholder: `${t("labels.choose")} ${t("labels.tickets")}`,
    type: "select",
    getEndpoint: "tickets",
    multiple: true,
  },
  {
    key: "gender",
    label: t("labels.gender"),
    placeholder: `${t("labels.choose")} ${t("labels.gender")}`,
    options: GENDERS_OPTIONS,
    type: "select",
  },
];
</script>
