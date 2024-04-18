<template>
    <transition name="modal-fade">
        <div class="modal-backdrop">
            <div class="modal">
                <header class="modal-header">
                    <slot name="header">
                        Add Product
                    </slot>
                    <button type="button" class="btn-close" @click="close" aria-label="Close modal">
                        x
                    </button>
                </header>

                <form @submit.prevent="handleSubmit">
                    <section class="modal-body">
                        <input class="modal-field" type="text" placeholder="Product Name" v-model="name" required />
                        <input class="modal-field" type="text" placeholder="Description" v-model="desc" required />
                        <div>
                            <label for="txtPrice">Price:</label>
                            <input class="modal-field" type="number" step="0.01" id="txtPrice" v-model.number="price" required />
                        </div>

                    </section>

                    <footer class="modal-footer">
                        <input type="submit" class="btn-green" value="Save">
                    </footer>
                </form>
            </div>
        </div>
    </transition>
</template>

<script>
export default {
    name: 'EditModal',

    data() {
        return {
            name: '',
            desc: '',
            price: 0
        }
    },
    methods: {
        handleSubmit() {

            // Validation for price
            if (this.price <= 0) {
                alert("Invalid Price");
                return;
            }
            this.close();
        },
        close() {
            let newProduct = {
                name: this.name,
                desc: this.desc,
                price: this.price
            }
            this.$emit('close', newProduct);
        },
    },
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

div .modal-field{
    margin-left: 0.2rem;
}
</style>