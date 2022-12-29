<template>
    <section>
        <TransitionGroup name="list" tag="ul">
            <li v-for="(todoItem, index) in propsdata" :key="index" class="shadow">
                <i class="checkBtn fas fa-check" aria-hidden="true"></i>
                {{ todoItem }}
                <span class="removeBtn" type="button" @click="removeTodo(index)">
                    <i class="fas fa-trash-alt" aria-hidden="true"></i>
                </span>
            </li>
        </TransitionGroup>
    </section>
</template>
<script>
export default {
    props: ['propsdata'],
    methods: {
        removeTodo: function(index) {
            console.log('delete at : ' + index);
            this.$emit('removeTodo', index);
        }
    }
}
</script>
<style scoped>
    .list-enter-active, .list-leave-active {
        transition: all 1s;
    }

    .list-enter, .list-leave-to {
        opacity: 0;
        transform: translateY(30px);
    }

    ul {
        list-style: none;
        padding-left: 0px;
        margin-top: 0px;
        text-align: left;
    }

    li {
        display: flex;
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5rem 0;
        padding: 0 0.9rem;
        background: white;
        border-radius: 5px;
    }

    .checkBtn {
        line-height: 45px;
        color: #62acde;
        margin-right: 5px;
    }

    .removeBtn {
        margin-left: auto;
        color: #de4343;
    }
</style>