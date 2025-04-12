<script setup>
import contactsInfo from "./contacts.json";
import { ref } from "vue";

const contacts = ref(contactsInfo.slice(5, 10));
</script>


<template>
    <div class="app">
        <h1>IronContacts</h1>
        <table>
        <tr>
            <td class="title">Picture</td>
            <td class="title">Name</td>
            <td class="title">Popularity</td>
            <td class="title">Won an Oscar</td>
            <td class="title">Won an Emmy</td>
        </tr>
        <tr v-for="(contact , i) in contacts" :key="i">
            <td>
                <img :src="contact.pictureUrl" />
            </td>
            <td>{{ contact.name }}</td>
            <td>{{ parseFloat(contact.popularity).toFixed(2) }}</td>
            <td v-if="contact.wonOscar">🏆</td>
            <td v-if="contact.wonEmmy">🏆</td>
        </tr>
    </table>
    </div>
</template>


<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: sans-serif;
}

.app {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    h1 {
        margin-top: 1rem;
        padding: 2rem;
        font-size: 3rem;
    }

    .title {
        padding: 1rem;
        font-size: 2rem;
        font-weight: bold;
        text-align: center;
    }

    td {
        font-size: 1.7rem;
        text-align: center;
    }

    img {
    height: 10rem;
    }
}
</style>
