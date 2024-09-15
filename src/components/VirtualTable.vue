<script>
import { ref, computed, onMounted, onUnmounted } from "vue";

export default {
  name: "HorizontalVirtualTable",
  props: {
    columns: Array,
    rows: Array,
    columnWidth: {
      type: Number,
      default: 150,
    },
  },
  setup(props) {
    const tableContainer = ref(null);
    const containerWidth = ref(0);
    const scrollLeft = ref(0);
    const prevEndIndex = ref(0);

    const totalWidth = computed(() => props.columns.length * props.columnWidth);

    const endIndex = computed(() => {
      const currentEndIndex = Math.ceil(
        (scrollLeft.value + containerWidth.value) / props.columnWidth
      );
      if (currentEndIndex > prevEndIndex.value) {
        prevEndIndex.value = currentEndIndex;
        return currentEndIndex;
      } else {
        return prevEndIndex.value;
      }
    });

    const visibleColumns = computed(() => {
      return props.columns.slice(0, endIndex.value);
    });

    const onScroll = (event) => {
      scrollLeft.value = event.target.scrollLeft;
    };

    const updateContainerWidth = () => {
      if (tableContainer.value) {
        // 這裡有需要把 containerWidth.value設定為tableContainer.value.clientWidth的原因是
        // 螢幕變化時有機會讓table的寬度跟著變
        containerWidth.value = tableContainer.value.clientWidth;
      }
    };

    onMounted(() => {
      updateContainerWidth();
      window.addEventListener("resize", updateContainerWidth);
    });

    onUnmounted(() => {
      window.removeEventListener("resize", updateContainerWidth);
    });

    return {
      tableContainer,
      totalWidth,
      visibleColumns,
      onScroll,
    };
  },
};
</script>

<template>
  <div class="horizontal-virtual-table" ref="tableContainer" @scroll="onScroll">
    <div class="table-content" :style="{ width: totalWidth + 'px' }">
      <table>
        <thead>
          <tr>
            <th
              v-for="column in visibleColumns"
              :key="column.id"
              :style="{ width: $props.columnWidth + 'px' }"
            >
              {{ column.title }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="row in rows" :key="row.id">
            <td
              v-for="column in visibleColumns"
              :key="column.id"
              :style="{ width: $props.columnWidth + 'px' }"
            >
              {{ row[column.key] }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
.horizontal-virtual-table {
  width: 80vh;
  max-width: 1000px;
  overflow-x: auto;
  overflow-y: hidden;
}
.table-content {
  overflow-x: hidden;
}
table {
  table-layout: fixed;
  border-collapse: collapse;
}
th,
td {
  padding: 8px;
  border: 1px solid #ddd;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>
