<template>
<div class="wrapper" ref="modal_wrapper">
    <div class="modal">
        <div class="modal__header">
            <div class="modal__header-text">Откликнуться</div>
            <span class="modal__header-close" @click="close">&times;</span>
        </div>
        <div class="modal__body">
            <form class="modal__form">
                <div class="modal__form-surname">
                    <label for="sername">Фамилия</label>
                    <input type="text" id="surname" placeholder="Фамилия">
                </div>
                <div class="modal__form-firstname">
                    <label for="firstname">Имя</label>
                    <input type="text" id="firstname" placeholder="Имя">
                </div>
                <div class="modal__form-patronymic">
                    <label for="patronymic">Отчество</label>
                    <input type="text" id="patronymic" placeholder="Отчество">
                </div>
                <div class="modal__form-phone">
                    <label for="phone">Фамилия</label>
                    <input type="text" id="phone" placeholder="+7(000)000-00-00">
                </div>
                <div class="modal__form-approv">
                    <input class="modal__form-checkbox" type="checkbox" value="Согласие">
                    <div class="modal__form-checkdescr">Я даю согласие на обработку своих персональных данных в соответствие с
                        <a href="#">положением об обработке персональных данных</a>.
                    </div>
                </div>
                <button class="modal__btn" disabled>Откликнуться</button>
         </form>
        </div>
    </div>
</div>
    
</template>

<script>


export default {
    name: "ModalForm",
    props: {

    },
    methods: {
        close() {
            console.log(123)
            this.$emit("closeModal")
        }
    },
    mounted() {
        let vm = this;
        document.addEventListener ('click', function(item) {
            if(item.target === vm.$refs['modal_wrapper']) {
                vm.close()
            }
        })

    },  
}
</script>


<style scoped>

.wrapper {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgba(64, 64, 64, 0.7);
    z-index: 12;

}
.modal {
    position: fixed;
    width: 400px;
    z-index: 20;
    border-radius: 3px;
    background-color: #fff;
    padding: 10px 20px;

}
.modal__header {
    padding-bottom: 10px;
}
.modal__header-text {
    display: inline;
    font-size: 1.5rem;
    position: relative;
}

.modal__header-close {
    position: absolute;
    font-weight: 600;
    right: 20px;
    cursor: pointer;
}

.modal__form-surname, .modal__form-firstname, .modal__form-patronymic, .modal__form-phone {
    position: relative;
    width: 100%;
}

label, input {
  display: block;
  margin-top: 1rem;
}

input[type=text] {
  z-index: 1;
  width: 100%;
  height: 40px;
  padding: 10px;
  border: 1px #a7a7a7 solid;
  border-radius: 2px;
  font-weight: 600;
}

label {
  position: absolute;
  top: -22px;
  left: 10px;
  z-index: 2;
  font-size: 0.7rem;
  color: #a7a7a7;
  padding: 0 6px;
  background-color: #fff;
}

.modal__form-phone input{
    letter-spacing: 1px;
}

.modal__form-approv {
    padding-top: 10px;
    font-size: 0.8rem;
    display: flex;
    justify-content: flex-start;
    align-items: flex-start;
}

.modal__form-checkbox {
    margin-top: 0;
    margin-right: 10px;
}

a {
    text-decoration: none;
}

.modal__btn {
    margin-top: 20px;
    margin-bottom: 10px;
    width: 40%;
    padding: 20px;
    border: 2px #fd7f23 solid;
    background-color: #fd7f23;
    color: white;
    border-radius: 3px;
    cursor: pointer;
}
.modal__btn[disabled] {
    cursor: auto;
    background-color: rgba(253, 127, 35, 0.6);
    border: none;
}


</style>