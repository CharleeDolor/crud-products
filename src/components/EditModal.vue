<template>
    <transition name="modal-fade">
        <div class="modal-backdrop">
            <div class="modal">
                <header class="modal-header">
                    <slot name="header">
                        <p class="header-title">Edit Product</p>
                    </slot>
                    <button type="button" class="btn-close" @click="closeDefault" aria-label="Close modal">
                        x
                    </button>
                </header>

                <form @submit.prevent="handleSubmit">
                    <section class="modal-body">
                        <div class="modal-group">
                            <label for="txtName">Name:</label>
                            <input id="txtName" class="modal-field" type="text" v-model="name" required/>
                        </div>

                        <div class="modal-group">
                            <label for="txtDesc">Description:</label>
                            <input id="txtDesc" class="modal-field" type="text" v-model="desc" required/>
                        </div>

                        <div class="modal-group">
                            <label for="txtPrice">Price:</label>
                            <input id="txtPrice" class="modal-field" type="number" v-model.number="price" step="0.01" required/>
                        </div>
                        
                        
                        
                    </section>

                    <footer class="modal-footer">
                        <input type="submit" value="Save" class="btn-save">
                    </footer>
                </form>
            </div>
        </div>
    </transition>
</template>

<script>
export default {
    name: 'EditModal',
    props: {
        product: {
            type: Object,
        }
    },

    mounted() {
        this.name = this.product.name;
        this.desc = this.product.desc;
        this.price = this.product.price;
    },

    data() {
        return {
            name: '',
            desc: '',
            price: 0
        }
    },
    methods: {
        handleSubmit(){
            this.close();
        },
        close() {
            let editedProduct = {
                id: this.product.id,
                name: this.name,
                desc: this.desc,
                price: this.price
            }
            this.$emit('close', editedProduct);
        },

        closeDefault(){
            this.$emit('closeDefault');
        },
    }
};
</script>

<style>
.modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal {
    background: #FFFFFF;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
}

.modal-header,
.modal-footer {
    padding: 15px;
    display: flex;
}

.modal-header {
    position: relative;
    border-bottom: 1px solid #eeeeee;
    color: #4AAE9B;
    justify-content: space-between;
}

.modal-footer {
    border-top: 1px solid #eeeeee;
    flex-direction: column;
    justify-content: flex-end;
}

.modal-body {
    position: relative;
    padding: 20px 10px;
    display: flex;
    flex-direction: column;
}

.btn-close {
    position: absolute;
    top: 0;
    right: 0;
    border: none;
    font-size: 20px;
    padding: 10px;
    cursor: pointer;
    font-weight: bold;
    color: #4AAE9B;
    background: transparent;
}

.btn-green {
    color: white;
    background: #4AAE9B;
    border: 1px solid #4AAE9B;
    border-radius: 2px;
}

.modal-fade-enter,
.modal-fade-leave-to {
    opacity: 0;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
    transition: opacity .5s ease;
}
</style>