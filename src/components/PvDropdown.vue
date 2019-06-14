<template>
  <div class="dropdown">
    <button @click.prevent="showDropdown = !showDropdown" class="dropdown__btn">Add filter</button>
    <transition name="slide-fade">
      <ul class="dropdown__menu" v-if="showDropdown">
        <li
          class="dropdown__item"
          v-for="(option, index) in options"
          :key="index"
          @click.prevent="sendOptionToFilters(option)"
        >{{ option }}</li>
      </ul>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      showDropdown: false
    };
  },

  methods: {
    sendOptionToFilters(option) {
      this.$emit("option", option);
      this.showDropdown = false;
    }
  }
};
</script>

<style lang="scss" scoped>
.dropdown {
  position: relative;
  border-radius: 0 0 8px 8px;
  margin: 0 1rem;
  width: auto;
}

.dropdown__btn {
  position: relative;
  background-color: transparent;
  border: 1px solid #007132;
  font-size: 1rem;
  padding: 0.5rem 1rem;
  transition: background-color 0.5s ease;
  display: inline-block;
  width: auto;
  display: flex;
  align-items: center;
}

.dropdown__btn::after {
  content: "+";
  background-color: #007132;
  border-radius: 50%;
  color: #fff;
  display: block;
  width: 10px;
  height: 14px;
  margin-left: 5px;
  padding: 0 5px 5px;
}

.dropdown__btn:hover {
  background-color: #007132;
  color: #fff;
  cursor: pointer;
}

.dropdown__btn:hover::after {
  background-color: #fff;
  color: #007132;
}

.dropdown__btn:focus {
  outline: none;
}

.dropdown__menu {
  position: absolute;
  top: 2rem;
  display: block;
  list-style: none;
  padding-left: 0;
  width: auto;
}

.dropdown__item {
  background-color: #9b9f9f;
  border-bottom: 1px solid darken(#9b9f9f, 15%);
  color: #fff;
  cursor: pointer;
  padding: 1rem;
  text-transform: capitalize;
  width: 100%;
}

.dropdown__item:hover {
  background-color: #00a248;
}

// Transitions
.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-leave-active {
  transition: all 0.2s ease;
}
.slide-fade-enter {
  transform: translateY(-50px);
  opacity: 0;
}
.slide-fade-leave-to {
  transform: translateY(-50px);
  opacity: 0;
}
</style>