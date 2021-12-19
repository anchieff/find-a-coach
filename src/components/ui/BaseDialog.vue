<template>
    <teleport to="body">
        <div v-if="show" @click="tryClose" class="backdrop"></div>
        <transition name="dialog">
            <dialog
                class="rounded-xl fixed p-0 m-0 bg-white shadow-lg"
                open
                v-if="show"
            >
                <header class="bg-purple-800 text-white w-full px-4 pt-3 pb-1">
                    <slot name="header">
                        <h2 class="text-2xl mb-3 font-medium">{{ title }}</h2>
                    </slot>
                </header>
                <section class="p-4">
                    <slot></slot>
                </section>
                <menu v-if="!fixed">
                    <slot name="actions">
                        <base-button @click="tryClose" mode="main">
                            Close
                        </base-button>
                    </slot>
                </menu>
            </dialog>
        </transition>
    </teleport>
</template>

<script>
export default {
    props: {
        show: {
            type: Boolean,
            required: true,
        },
        title: {
            type: String,
            required: false,
        },
        fixed: {
            type: Boolean,
            required: false,
            default: false,
        },
    },
    emits: ['close'],
    methods: {
        tryClose() {
            if (this.fixed) {
                return
            }
            this.$emit('close')
        },
    },
}
</script>

<style scoped>
.backdrop {
    position: fixed;
    top: 0;
    left: 0;
    height: 100vh;
    width: 100%;
    background-color: rgba(0, 0, 0, 0.75);
    z-index: 10;
}

dialog {
    top: 20vh;
    left: 10%;
    width: 80%;
    z-index: 100;
    border: none;
    overflow: hidden;
}

menu {
    padding: 1rem;
    display: flex;
    justify-content: flex-end;
    margin: 0;
}

.dialog-enter-from,
.dialog-leave-to {
    opacity: 0;
    transform: scale(0.8);
}

.dialog-enter-active {
    transition: all 0.3s ease-out;
}

.dialog-leave-active {
    transition: all 0.3s ease-in;
}

.dialog-enter-to,
.dialog-leave-from {
    opacity: 1;
    transform: scale(1);
}

@media (min-width: 768px) {
    dialog {
        left: calc(50% - 20rem);
        width: 40rem;
    }
}
</style>
