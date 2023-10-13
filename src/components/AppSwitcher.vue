<template>
  <div class="switcher">
    <input
      type="checkbox"
      :checked="check"
      class="switcher__input"
      :name="name"
      :id="name"
      @change="$emit('update', $event.target.checked)"
    />
    <label class="switcher__label" :for="name"></label>
  </div>
</template>

<script>
export default {
  name: "AppSwitcher",
  props: {
    name: String,
    check: Boolean,
  },
};
</script>

<style scoped>
.switcher__input {
  display: none;
}
.switcher__label {
  width: 37px;
  height: 17px;
  border-radius: 20px;
  position: relative;
  cursor: pointer;
  display: inline-block;
  background-color: #fff;
  border: 1px solid #cdced8;
  transition: 0.3s;
}
.switcher__label::after {
  content: "";
  position: absolute;
  display: block;
  width: 19px;
  height: 19px;
  box-sizing: border-box;
  background-color: #fdfdfd;
  border: 1px solid #cdced8;
  border-radius: 20px;
  top: -1px;
  left: -1px;
  transition: 0.3s;
  animation: switcher-off 0.3s ease both;
}
.switcher__input:checked + .switcher__label {
  background-color: #7d7aff;
  border: 1px solid #7d7aff;
}
.switcher__input:checked + .switcher__label::after {
  animation: switcher-on 0.3s ease both;
}
@keyframes switcher-off {
  0% {
    transform: translateX(20px);
  }
  100% {
    transform: translateX(0);
  }
}
@keyframes switcher-on {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(20px);
  }
}
</style>
