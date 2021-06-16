<template>
  <div>
      <select 
    @change="$emit('performSelectGenre', $event.target.value)"
    >
      <option disabled value="">Seleziona un genere</option>
      <option>All</option>
      <option v-for="genre,index in genresTypes" 
      :value="genre.id"
      :key="index">
            {{ genre.name }}
      </option> 
   </select>
  </div>
</template>

<script>
export default {
    name:"Select",
    props: [ "genresTypes" ]
}
</script>

<style lang="scss" scoped>
div{
    position:absolute;
    top:20px;
    right:80px;
}
</style>