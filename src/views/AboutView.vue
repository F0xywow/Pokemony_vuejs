<script>

const listof = [
  {
    id: 1,
    name: 'John Doe',
    email: 'dsadas'
  },
  {
    id: 2,
    name: 'Jane Doe',
    email: 'dsadas'
  },
  {
    id: 3,
    name: 'John Smith',
    email: 'dsadas'
  },
  {
    id: 4,
    name: 'Jane Smith',
    email: 'dsadas'
  }
]

</script>

<template>
  <main>
    <li v-for="item in listof">
    {{ id }} -- {{ name }} -- {{ email }}
    </li>
  </main>
</template>


