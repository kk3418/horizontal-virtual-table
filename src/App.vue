<script setup>
import { ref } from "vue";
import VirtualTable from "@/components/VirtualTable.vue";

const columns = ref([
  { id: 1, title: "Name", key: "name" },
  { id: 2, title: "Age", key: "age" },
  { id: 3, title: "Address", key: "address" },
  { id: 4, title: "City", key: "city" },
  { id: 5, title: "Country", key: "country" },
  { id: 6, title: "Phone", key: "phone" },
  { id: 7, title: "Email", key: "email" },
  { id: 8, title: "Company", key: "company" },
  { id: 9, title: "Job Title", key: "jobTitle" },
  { id: 10, title: "Department", key: "department" },
  { id: 11, title: "Date of Birth", key: "dob" },
  { id: 12, title: "Friend A", key: "friend_a" },
  { id: 13, title: "Friend B", key: "friend_b" },
  { id: 14, title: "2024-09-01", key: "2024-09-01" },
  { id: 15, title: "2024-09-02", key: "2024-09-02" },
  { id: 16, title: "2024-09-03", key: "2024-09-03" },
  { id: 17, title: "2024-09-04", key: "2024-09-04" },
  { id: 18, title: "2024-09-05", key: "2024-09-05" },
  { id: 19, title: "2024-09-06", key: "2024-09-06" },
  { id: 20, title: "2024-09-07", key: "2024-09-07" },
]);

const rows = ref([
  {
    id: 1,
    name: "John Doe",
    age: 30,
    address: "123 Main St",
    city: "Springfield",
    country: "USA",
    phone: "555-1234",
    email: "k1o31@mail.com",
    company: "ABC Inc",
    jobTitle: "Software Engineer",
    department: "Engineering",
    dob: "01/01/1990",
    friend_a: "Jane Doe",
    friend_b: "Jim Doe",
    "2024-09-01": "a",
    "2024-09-02": "b",
    "2024-09-03": "c",
    "2024-09-04": "d",
    "2024-09-05": "e",
    "2024-09-06": "f",
    "2024-09-07": "g",
  },
  {
    id: 2,
    name: "Jane Doe",
    age: 25,
    address: "456 Elm St",
    city: "Springfield",
    country: "USA",
    phone: "555-5678",
    email: "jfoa@mail.com",
    company: "XYZ Corp",
    jobTitle: "Product Manager",
    department: "Product",
    dob: "01/01/1995",
    friend_a: "John Doe",
    friend_b: "Jim Doe",
    "2024-09-01": "a",
    "2024-09-02": "b",
    "2024-09-03": "c",
    "2024-09-04": "d",
    "2024-09-05": "e",
    "2024-09-06": "f",
    "2024-09-07": "g",
  },
]);
</script>

<template>
  <div>
    <VirtualTable :columns="columns" :rows="rows" :columnWidth="200" />
  </div>
</template>

<style scoped>
</style>
