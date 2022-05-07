<template>
<div class="base-card">
    <div class="card__img">
        <img :src="img" class="img-fluid">
    </div>
    <div class="card__id">#{{ pkmnid }}</div>
    <div class="card__name">{{ name }}</div>
</div>
       
</template>

<script>
export default {
name: 'BaseCard',
  props: {
    name: {
      type: String,
      default: ""
    },
    img: {
      type: String,
      default: ""
    },
    id: {
      type: Number
    }
  },
  computed: {
      pkmnid() {
      return `${this.id}`
    }
  }
}
</script>
<style scoped>
.base-card {
    display: flex;
    align-items: center;
    flex-direction: column;
    font-size: 13px;
    height: 100%;
    padding: 5px;
    position: relative;
}

.card__id {
    position: absolute;
    top: 0;
    right: 0;
    padding: 0 5px;
    background-color: #004385;
}

.card__img img{
    max-height: 50px;
    margin-right: 10px;
}
</style>