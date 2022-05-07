<template>
<div class="base-card card--hidden">
  <div class="card__img">
        <img src="../../assets/question-mark.png" class="img-fluid">
    </div>
</div>
</template>

<script>
export default {
name: 'HiddenCard',
  props: {
    name: {
      type: String,
      default: ""
    },
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
}

.card__img {
    height: 100%;
    margin-top: 10px;
}

.card__img img {
    max-width: 30px;
}
</style>