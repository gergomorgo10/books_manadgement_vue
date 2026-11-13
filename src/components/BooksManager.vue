<script setup>
import { getBooks } from '../api/books';
</script>

<script>
export default {
    name: "BooksManager",
    data(){
        return{
            books: [],
        };
    },
    methods: {
        async loadBooks(){
            this.books = await getBooks();
        },
    },
    mounted(){
        this.loadBooks();
    }
};
</script>

<template>
    <main class=" flex justify-center items-center flex-col">
        <h1 class="">könyvtár kezelőfelület</h1>

        <table class="">
            <thead class="">
                <tr class="">
                    <th class="">azonosító</th>
                    <th class="">címe</th>
                    <th class="">szerző</th>
                    <th class="">megjelenés éve</th>
                    <th class="">műveletek</th>
                </tr>
            </thead>
            <tbody class="">
                <tr class="" v-for="book in books" :key="book.id">
                    <td class="">{{ book.id }}</td>
                    <td class="">{{ book.title }}</td>
                    <td class="">{{ book.author }}</td>
                    <td class="">{{ book.year }}</td>
                    <td class="">-</td>
                </tr>
            </tbody>
        </table>
    </main>
</template>