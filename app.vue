<template>
  <div class="todo">
    <div class="todo__background">
      <img src="/bg-desktop-dark.jpg" alt="background">
    </div>
    <div class="todo__container">
      <div class="todo__header">
        <div class="todo__title">TODO</div>
        <button class="btn-secondary todo__theme">
          <img src="~/assets/images/icon-sun.svg" alt="theme">
        </button>
      </div>
      <div class="todo__add">
        <div class="todo__add-graphic"></div>
        <div class="todo__add-input">
          <input type="text" placeholder="Create a new todo...">
        </div>
      </div>
      <ul class="todo__list">
        <li class="todo__list-item">
          <label class="todo__item-checkbox">One
            <input type="checkbox">
            <span class="todo__item-checkmark"></span>
          </label>
          <button class="btn-secondary">
            <img src="~/assets/images/icon-cross.svg" alt="remove">
          </button>
        </li>
        <li class="todo__list-item">
          <label class="todo__item-checkbox">One
            <input type="checkbox">
            <span class="todo__item-checkmark"></span>
          </label>
          <button class="btn-secondary">
            <img src="~/assets/images/icon-cross.svg" alt="remove">
          </button>
        </li>
        <li class="todo__list-item">
          <label class="todo__item-checkbox">One
            <input type="checkbox">
            <span class="todo__item-checkmark"></span>
          </label>
          <button class="btn-secondary">
            <img src="~/assets/images/icon-cross.svg" alt="remove">
          </button>
        </li>
        <li class="todo__list-item">
          <label class="todo__item-checkbox">One
            <input type="checkbox">
            <span class="todo__item-checkmark"></span>
          </label>
          <button class="btn-secondary">
            <img src="~/assets/images/icon-cross.svg" alt="remove">
          </button>
        </li>
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
      input {
        background-color: transparent;
        border: none;
        color: #ccc;

        &:focus {
          outline: none;
        }
      }
    }
  }

  &__list {
    list-style: none;
    margin: 0 0 30px 0;
    padding: 0;

    &-item {
      padding: 20px;
      border-bottom: 1px solid #575555;
      display: flex;
      align-items: center;
      justify-content: space-between;

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
  }

  /* Customize the label (the container) */
  &__item-checkbox {
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
    &:hover input ~ .checkmark {
      background-color: #ccc;
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

        /* Show the checkmark when checked */
        &:after {
          display: block;
        }
      }
    }
  }

  /* Create a custom checkbox */
  &__item-checkmark {
    position: absolute;
    top: 0;
    left: 0;
    height: 24px;
    width: 24px;
    background-color: #eee;
    border-radius: 50%;

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

  &__dnd {
    color: #7d7d7d;
    text-align: center;
  }

  @media only screen and (max-width: 768px) {
    &__container {
      width: calc(100% - 48px);
      margin-top: 60px;
    }

    &__list {
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
}
</style>