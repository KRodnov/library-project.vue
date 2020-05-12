<template>
    <div class="book-container">
    <div v-bind:class="`book ${item.status}`">
        <h4>Книга # {{item.id}} - {{bookReedStatus}}</h4>
        <h1>"{{item.nameBook}}"</h1>
        <h4>{{item.authorNameBook}} {{item.authorSurnameBook}}</h4>
        <h4>{{item.yearBook}}</h4>
        <h4>{{item.genreBook}}</h4>
            <button v-if="item.status!='finished'" v-on:click="finishBook">Прочитано</button>
            <button  v-on:click="editBook">Редактировать</button>
            <button  v-on:click="deleteBook">Удалить книгу</button>
    </div>
    </div>

</template>

<script>
    export default {
        name: "book",
        props: ['item','books'],

        computed: {
            bookReedStatus: function () {

                switch (this.item.status) {
                    case 'pending':
                        return 'Не прочитано';
                        case 'finished':
                            return 'Прочитано'
                }

            }
        },
        methods: {
            editBook: function () {
            this.$emit('editBook', this.item.id)
            },
            deleteBook: function () {
            this.$emit('deleteBook', this.item.id)
            },
            finishBook: function () {
                this.$emit('finishBook',this.item.id)
            }
        }


    }
</script>

<style>

    .book-container {
        display: flex;
        width: 100%;
    }

    .book {

        min-width: 300px;
        min-height: 300px;
        border: 1px solid black;
        margin: 5px;
        padding: 5px;
        border-radius: 6px;
        flex-direction: row;

    }

    .book.pending {
        background-color: crimson;
    }
    .book.finished {
        background-color: aqua;
    }


</style>