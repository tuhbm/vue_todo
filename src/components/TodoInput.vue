<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
        <span class="addContainer" @click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>

        <Modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">
                경고!
                <i class="closeModalBtn fas fa-times-circle"
                   @click="showModal = false"></i>
            </h3>

            <div slot="body">
                입력값이 없습니다.
            </div>

        </Modal>
    </div>
</template>

<script>
import Modal from './common/Modal';

export default {
    data() {
        return {
            newTodoItem: '',
            showModal: false
        };
    },
    methods: {
        addTodo() {
            if (this.newTodoItem !== '') {
                const text = this.newTodoItem.trim();
                this.$store.commit('addOneItem', text);
                this.clearInput();
            } else {
                this.showModal = !this.showModal;
            }
        },
        clearInput() {
            this.newTodoItem = '';
        }
    },
    components: {
        Modal
    }
};
</script>

<style scoped>
    input:focus {
        outline: none;
    }

    .inputBox {
        background: #fff;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }

    .inputBox input {
        border-style: none;
        font-size: 0.9rem
    }

    .addContainer {
        float: right;
        background: linear-gradient(to right, #6478FB, #8763FB);
        display: block;
        width: 3rem;
        border-radius: 0 5px 5px 0;
        cursor: pointer;
    }

    .addBtn {
        color: #fff;
        vertical-align: middle;
    }

    .closeModalBtn {
        position: absolute;
        top: 10px;
        right: 10px;
        color: #42b983;
        cursor: pointer;
    }
</style>
