<script setup>
import { inject } from 'vue';

defineProps(['item']);

const { changeState, remove } = inject('list');
</script>

<template>
    <li :class="{ 'todo__list-item--completed': item.completed }">
        <label class="todo__item-checkbox">
            {{ item.name }}
            <input type="checkbox" @click="changeState(item)">
            <span class="todo__item-checkmark"></span>
        </label>
        <button class="btn-secondary" @click="remove(item)">
            <img src="~/assets/images/icon-cross.svg" alt="remove">
        </button>
    </li>
</template>

<style lang="scss" scoped>
/* Customize the label (the container) */
.todo__item-checkbox {
    display: block;
    position: relative;
    padding-left: 46px;
    cursor: pointer;
    font-size: 16px;
    user-select: none;
    color: #ccc;
    line-height: 24px;
    flex-grow: 1;

    /* On mouse-over, add a grey background color */
    &:hover {
      input {
        &:checked ~ .todo__item-checkmark:before {
          background: linear-gradient(to right, #7eb6e6 0%, #a182ef 100%);
        }
      }
      
      .todo__item-checkmark {
        background: linear-gradient(to right, #7eb6e6 0%, #a182ef 100%) !important;
      }
    }

    /* Hide the browser's default checkbox */
    input {
      position: absolute;
      opacity: 0;
      cursor: pointer;
      height: 0;
      width: 0;

      /* When the checkbox is checked, add a blue background */
      &:checked ~ .todo__item-checkmark  {
        background: linear-gradient(to right, #7eb6e6 0%, #a182ef 100%);

        &:before {
          background: inherit;
        }

        /* Show the checkmark when checked */
        &:after {
          display: block;
        }
      }
    }
  }

/* Create a custom checkbox */
.todo__item-checkmark {
    position: absolute;
    top: 0;
    left: 0;
    height: 24px;
    width: 24px;
    border-radius: 50%;
    background: linear-gradient(to right, #4a4a4a 0%, #4a4a4a 100%);
    border: none;

    &:before {
      content: "";
      background-color: #25273d;
      width: calc(100% - 2px);
      height: calc(100% - 2px);
      position: absolute;
      border-radius: 50%;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

    /* Create the checkmark/indicator (hidden when not checked) */
    /* Style the checkmark/indicator */
    &:after {
      content: "";
      position: absolute;
      display: none;
      left: 10px;
      top: 6px;
      width: 5px;
      height: 10px;
      border: solid white;
      border-width: 0 3px 3px 0;
      -webkit-transform: rotate(45deg);
      -ms-transform: rotate(45deg);
      transform: rotate(45deg);
    }
}
</style>