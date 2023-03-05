<script setup>
defineProps(['items']);

</script>

<template>
    <ul class="todo__list">
        <Item class="todo__list-item" v-for="item in items" :key="item.name" :item="item" />
        
        <div class="todo__list-actions">
            <div class="todo__list-left">5 items left</div>
            <div class="todo__list-statuses">
            <button class="btn-secondary todo__list-status">All</button>
            <button class="btn-secondary todo__list-status">Active</button>
            <button class="btn-secondary todo__list-status">Compelete</button>
            </div>
            <button class="btn-secondary todo__list-clear">Clear Completed</button>
        </div>
    </ul>
</template>

<style lang="scss" scope>
.todo__list {
    list-style: none;
    margin: 0 0 30px 0;
    padding: 0;

    &-item {
      padding: 20px;
      border-bottom: 1px solid #343232;
      display: flex;
      align-items: center;
      justify-content: space-between;

      &--completed {
        text-decoration: line-through;
      }

      .btn-secondary {
        display: flex;
        cursor: pointer;
      }
    }

    &-actions {
      display: flex;
      justify-content: space-between;
      padding: 20px;
      color: #7d7d7d;
      align-items: center;
      font-weight: 500;
    }

    &-left {
      font-size: 14px;
    }

    &-status,
    &-clear {
      color: inherit;
      cursor: pointer;

      &:hover {
        color: #7eb6e6;
      }
    }

    @media only screen and (max-width: 768px) {
        margin-bottom: 120px;

        &-actions {
            flex-wrap: wrap;
            position: relative;
        }

        &-statuses {
            flex-basis: 100%;
            order: 1;
            display: flex;
            justify-content: center;
            position: absolute;
            top: 80px;
            border-radius: 4px;
            background-color: #25273d;
            width: 100%;
            left: 0;
            padding: 20px;
        }
    }
}
</style>