<template>
    <transition name="modal-fade">
        <div class="modal-backdrop">
            <div class="modal">
                <header class="modal-header">
                    <slot name="header">
                        Add Product
                    </slot>
                    <button type="button" class="btn-close" @click="closeDefault" aria-label="Close modal">
                        x
                    </button>
                </header>

                <form ref="form" @submit.prevent="animateSave">
                    <section class="modal-body">
                        <div class="modal-group">
                            <label for="txtName">Name: </label>
                            <span class="error" v-if="errName.length > 0">{{ errName }}</span>
                            <input class="modal-field" id="txtName" type="text" v-model="name" required />
                        </div>

                        <div class="modal-group">
                            <label for="txtDesc">Description:</label>
                            <span class="error" v-if="errDesc.length > 0">{{ errDesc }}</span>
                            <input class="modal-field" id="txtDesc" type="text" v-model="desc" required />
                        </div>

                        <div class="modal-group">
                            <label for="txtPrice">Price:</label>
                            <span class="error" v-if="errPrice.length > 0">{{ errPrice }}</span>
                            <input class="modal-field" type="number" id="txtPrice" min="0" v-model.number="price" required />
                        </div>

                    </section>

                    <footer class="modal-footer">
                        <button type="button" class="btn-green" @click="animateSave">
                            <span v-for="(letter, index) in saveText" :key="index"
                                :class="{ 'jump': saveAnimated[index] }">{{ letter }}</span>
                        </button>
                    </footer>
                </form>
            </div>
        </div>
    </transition>
</template>

<script>
export default {
    name: 'AddModal',

    data() {
        return {
            name: '',
            desc: '',
            price: 0,
            saveText: 'Save',
            saveAnimated: [false, false, false, false], // Array to track which letters to animate
            errName: '',
            errDesc: '',
            errPrice: '',
        }
    },
    methods: {
        close() {
            let newProduct = {
                name: this.name,
                desc: this.desc,
                price: this.price
            }
            this.$emit('close', newProduct);
        },

        closeDefault() {
            this.$emit('closeDefault');
        },

        animateSave() {
            // Validate form manually
            // if (!this.$refs.form.checkValidity()) {
            //     return false; // Prevent form submission
            // }

            // Animate the Save button
            this.saveAnimated = [false, false, false, false]; // Reset animation status
            setTimeout(() => {
                this.saveAnimated = [true, true, true, true]; // Trigger animation
                    // Your form submission logic here
            }, 5000);

            let newProduct = {
                name: this.name,
                desc: this.desc,
                price: this.price
            }

            // check if a field is empty 
            if (this.name == '' || this.desc == '' || this.price <= 0) {
                // Load error message base on what field is empty
                if (this.name == '') {
                    this.errName = "Name is required";
                } else {
                    this.errName = "";
                }

                if (this.desc == '') {
                    this.errDesc = "Description is required";
                } else {
                    this.errDesc = "";
                }

                if (this.price <= 0) {
                    this.errPrice = "Price is invalid";
                } else {
                    this.errPrice = "";
                }
                return;
            }
            this.$emit('close', newProduct);


        }
    },
};
</script>

<style>
@keyframes jumpAnimation {
    0% {
        transform: translateY(0);
    }

    25% {
        transform: translateY(-10px);
    }

    50% {
        transform: translateY(0);
    }

    75% {
        transform: translateY(-5px);
    }

    100% {
        transform: translateY(0);
    }
}

.jump {
    animation: jumpAnimation 1s ease;
}

.btn-green {
    color: white;
    background: transparent;
    border: 1px solid transparent;
    font-size: 20px;
    border-radius: 2px;
    padding: 10px 20px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    outline: none;
}

.btn-green span {
    display: inline-block;
    transition: transform 0.3s ease;
}

.btn-green:hover span {
    transform: translateY(-50%);
}

.table {
    display: flex;
    justify-content: center;
}

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
    justify-content: center;
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
    color: black;
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

.error {
    color: red;
}
</style>