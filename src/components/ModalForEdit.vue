<template>
  <div class="modal__background">
    <div class="modal">
      <div class="modal__text">
        <slot name="modalText">Редактирование поля:</slot>
      </div>
      <div class="modal__form">
        <slot name="form"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModalForEdit',
}
</script>


<style scoped lang="scss">
.modal__background {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
  .modal {
    background: #68c046;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
    padding: 20px;
    .modal__text {
      padding: 20px
    }
    .modal__form {
      .edit__first__field {
        margin-bottom: 10px;
        label {
          margin-right: 57px;
        }
      }
      .edit__second__field {
        label {
          margin-right: 5px;
        }
      }
      .modal__buttons {
        display: flex;
        justify-content: center;
        margin-top: 20px;
        padding: 20px;
        .modal__button_1 {
          margin-right: 50px;
          .btn__edit {
            width: 115px;
            height: 40px;
            background-color: rgb(100, 90, 197);
            border: 1px solid;
            cursor: pointer;
            outline: none;
            box-shadow: 2px 2px 10px 1px;
            &:hover {
              opacity: 0.9
            }
          }
        }
        .modal__button_2 {
          .btn__no {
            width: 100px;
            height: 40px;
            background-color: rgb(145, 16, 16);
            color: white;
            border: 1px solid;
            cursor: pointer;
            outline: none;
            box-shadow: 2px 2px 10px 1px;
            &:hover {
              opacity: 0.9
            }
          }
        }
      }
    }
  }
}

</style>
