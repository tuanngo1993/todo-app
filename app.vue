<script setup>
import { ref, provide } from 'vue';

const darkTheme = ref(true);
const newTask = ref('');
const listItems = ref([]);

function switchTheme() {
  darkTheme.value = !darkTheme.value;
}

function onSubmit() {
  if(newTask.value !== '') {
    listItems.value.push({
      name: newTask.value,
      completed: false
    });

    newTask.value = "";
  }
}

function changeState(item) {
  const indexItem = listItems.value.indexOf(item);
  listItems.value[indexItem].completed = !listItems.value[indexItem].completed;
}

function remove(item) {
  const indexItem = listItems.value.indexOf(item);
  listItems.value.splice(indexItem, 1);
}

provide('list', {
  changeState,
  remove
})
</script>

<template>
  <div class="todo" :class="{ light: !darkTheme }">
    <div class="todo__background">
      <img v-if="darkTheme" src="/bg-desktop-dark.jpg" alt="background">
      <img v-else src="/bg-desktop-light.jpg" alt="background">
    </div>
    <div class="todo__container">
      <div class="todo__header">
        <div class="todo__title">TODO</div>
        <button class="btn-secondary todo__theme" @click="switchTheme">
          <img v-if="darkTheme" src="~/assets/images/icon-sun.svg" alt="theme">
          <img v-else src="~/assets/images/icon-moon.svg" alt="theme">
        </button>
      </div>
      <form @submit.prevent="onSubmit" class="todo__add">
        <div class="todo__add-graphic"></div>
        <div class="todo__add-input">
          <input v-model="newTask" type="text" placeholder="Create a new todo...">
        </div>
      </form>
      <List :items="listItems" />
      <p class="todo__dnd">
        Drag and drop to reorder list
      </p>
    </div>
  </div>
</template>

<style lang="scss">
.todo {
  height: 100vh;
  background-color: #161622;
  display: flex;
  flex-direction: column;
  align-items: center;

  &__container {
    width: 550px;
    margin-top: 60px;
  }

  &__background {
    height: 40%;
    position: absolute;
    left: 0;
    right: 0;

    img {
      width: 100%;
      height: 100%;
    }
  }

  &__header {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: #fff;
    margin-bottom: 40px;
  }

  &__title {
    font-size: 40px;
    letter-spacing: 12px;
    font-weight: 700;
  }

  &__add,
  &__list {
    border-radius: 4px;
    background-color: #25273d;
    position: relative;
  }

  &__add {
    width: 100%;
    height: 60px;
    display: flex;
    align-items: center;
    gap: 20px;
    margin-bottom: 20px;
    padding: 0 20px;

    &-graphic {
      height: 24px;
      width: 24px;
      border: 1px solid #4a4a4a;
      border-radius: 50%;
    }

    &-input {
      flex-grow: 1;

      input {
        background-color: transparent;
        border: none;
        width: 100%;
        color: #ccc;

        &:focus {
          outline: none;
        }
      }
    }
  }

  &__dnd {
    color: #7d7d7d;
    text-align: center;
  }

  &.light {
    background-color: #fafafa;

    .todo__add,
    .todo__list {
      background-color: #fff;
    }

    .todo__add {
      &-graphic {
        border-color: #ccc;
      }

      &-input input {
        color: #7b7474;
      }
    }

    .todo__list {
      box-shadow: 1px 11px 13px 0px #f3e9e9;

      &-item {
        border-color: #e8e8e8;
      }
    }

    .todo__item {
      &-checkbox {
        color: #7b7474;
      }

      &-checkmark {
        background: linear-gradient(to right, #ccc 0%, #ccc 100%);

        &:before {
          background-color: #fff;
        }
      }
    }
  }

  @media only screen and (max-width: 768px) {
    &__container {
      width: calc(100% - 48px);
      margin-top: 60px;
    }

    &.light {
      .todo__list {
        &-statuses {
          background-color: #fff;
          box-shadow: 1px 11px 13px 0px #f3e9e9;
        }
      }
    }
  }
}
</style>