<template>
    <blockquote class="advice">
        <div class="advice__content">
            <h1>advice #{{ advice.id }}</h1>
            <p>"{{ advice.advice }}"</p>
        </div>
        <span class="advice__separator">
            <svg fill="none" viewBox="0 0 444 16" xmlns="http://www.w3.org/2000/svg">
              <path d="M0 8h196v1H0zM248 8h196v1H248z" fill="#4F5D74" />
              <rect fill="#CEE3E9" height="16" rx="3" width="6" x="212" />
              <rect fill="#CEE3E9" height="16" rx="3" width="6" x="226" />
            </svg>
        </span>
        <button :disabled="muted" @click="newAdvice" class="advice__roll-button">
            <svg fill="none" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                <path clip-rule="evenodd" d="M4 0h16c2.2081.002526 3.9975 1.79191 4 4v16c-.0025 2.2081-1.7919 3.9975-4 4H4c-2.20809-.0025-3.997474-1.7919-4-4V4C.002526 1.79191 1.79191.002526 4 0Zm2 16.5c0 .8284.67157 1.5 1.5 1.5S9 17.3284 9 16.5 8.32843 15 7.5 15 6 15.6716 6 16.5ZM7.5 9C6.67157 9 6 8.32843 6 7.5S6.67157 6 7.5 6 9 6.67157 9 7.5 8.32843 9 7.5 9Zm3 3c0 .8284.6716 1.5 1.5 1.5s1.5-.6716 1.5-1.5-.6716-1.5-1.5-1.5-1.5.6716-1.5 1.5Zm6 6c-.8284 0-1.5-.6716-1.5-1.5s.6716-1.5 1.5-1.5 1.5.6716 1.5 1.5-.6716 1.5-1.5 1.5ZM15 7.5c0 .82843.6716 1.5 1.5 1.5S18 8.32843 18 7.5 17.3284 6 16.5 6 15 6.67157 15 7.5Z" fill="currentColor" fill-rule="evenodd" />
            </svg>
        </button>
    </blockquote>
</template>

<script setup>
import axios from "axios"
import {onMounted, ref} from "vue"

const advice = ref({
    id: '117',
    advice: 'It is easy to sit up and take notice, what\'s difficult is getting up and taking action.'
})
const muted = ref(false)

async function newAdvice() {
    const response = await axios.get('https://api.adviceslip.com/advice').then(r => r.data)
    advice.value = response["slip"]
    muted.value = true
    console.log('new')
    handleMuted()
}

function handleMuted() {
    setTimeout(() => {
        muted.value = false
    }, 2000)
}

</script>