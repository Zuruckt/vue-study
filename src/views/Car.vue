<template>
  <div>
    <CarTable/>
  </div>
</template>

<script>
// @ is an alias to /src
import CarTable from "@/components/Car/CarTable";

export default {
  name: 'Home',
  components: {
    CarTable
  }
}
</script>
