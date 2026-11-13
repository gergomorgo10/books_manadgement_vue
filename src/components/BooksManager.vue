<script setup>
import { createBook, getBooks } from '../api/books';
</script>

<script>
export default {
    name: "BooksManager",
    data(){
        return{
            books: [],
            newBook: {
                title: "",
                author: "",
                year: 2000,
            }
        };
    },
    methods: {
        async loadBooks(){
            this.books = await getBooks();
        },
        async addBook(book){
            await createBook(book);
            await this.loadBooks();
        },
        async submitCreateBook(){
            await this.addBook(this.newBook);
        },
    },
    mounted(){
        this.loadBooks();
    }
};
</script>

<template>
    <main class=" flex justify-center items-center gap-2 flex-col">
        <h1 class="">könyvtár kezelőfelület</h1>

        <form class=" w-full m-10 border-2 border-stone-700 rounded-lg p-3 flex flex-col" @submit.prevent="submitCreateBook">
            <div class="flex flex-col">
            <label for="title" class="">könyv címe:</label>
            <input v-model="newBook.title" type="text" id="" name="title" class="border-2 border-stone-700 rounded-lg py-1 px-2">
            </div>

            <div class="flex flex-col">
            <label for="author" class="">könyv szerzője:</label>
            <input v-model="newBook.author" type="text" id="" name="author" class="border-2 border-stone-700 rounded-lg py-1 px-2">
            </div>

            <div class="flex flex-col">
            <label for="year" class="">könyv megjelenési éve:</label>
            <input v-model="newBook.year" type="number" name="year" class="border-2 border-stone-700 rounded-lg py-1 px-2" id="">
            </div>

            <button type="submit" class="border-2 border-stone-700 rounded-lg mt-4">Létrehozás</button>
        </form>

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