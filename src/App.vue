<script setup>
import contactsInfo from "./contacts.json";
import { ref } from "vue";

const contacts = ref(contactsInfo.slice(5, 10));

const addRandomContact = () => {
    const randomContact = contactsInfo[Math.floor(Math.random() * contactsInfo.length)];

    if (!contacts.value.includes(randomContact)) {
        contacts.value.push({...randomContact})
    }
}

const sortByName = () => {
    contacts.value.sort((a, b) => a.name.localeCompare(b.name));
}

const sortByPopularity = () => {
    contacts.value.sort((a, b) => parseFloat(b.popularity) - parseFloat(a.popularity))
}

const deleteContact = (contactId) => {
    contacts.value = contacts.value.filter(c => c.id !== contactId)
}
</script>


<template>
    <div class="app">
        <h1>IronContacts</h1>
        <div class="btns">
            <button @click="addRandomContact">Add Contact Button</button>
            <button @click="sortByName">Sort by Name</button>
            <button @click="sortByPopularity">Sort by Popularity</button>
        </div>
        <table>
        <tr>
            <td class="title">Picture</td>
            <td class="title">Name</td>
            <td class="title">Popularity</td>
            <td class="title">Won an Oscar</td>
            <td class="title">Won an Emmy</td>
        </tr>
        <tr class="contacts-list" v-for="(contact , i) in contacts" :key="i">
            <td>
                <img :src="contact.pictureUrl" />
            </td>
            <td>{{ contact.name }}</td>
            <td>{{ parseFloat(contact.popularity).toFixed(2) }}</td>
            <td v-if="contact.wonOscar">🏆</td>
            <td v-if="contact.wonEmmy">🏆</td>
            <button @click="deleteContact(contact.id)">Delete Contact</button>
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

    .btns {
        width: 100%;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }

    button {
        height: 40px;
        width: 80px;
    }
}
</style>
