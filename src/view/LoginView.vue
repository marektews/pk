<script setup>
import { ref, computed } from 'vue'
import LoginButton from '@/components/btns/LoginButton.vue'
import TitleView from '@/components/TitleView.vue'
import SelectDepartment from '@/components/SelectDepartment.vue'
import ValidityInputGroup from '@/components/input/ValidityInputGroup.vue'

const props = defineProps(['modelValue'])

const department = computed({
    get() {
        return props.modelValue
    },
    set(value) {
        emit('update:modelValue', value)
    }
})

const showAlert = ref(false)
const password = ref('')

const isLoginBtnEnabled = computed({
    get() { return department.value !== undefined && password.value.length > 0 }
})

const emit = defineEmits(['update:modelValue', 'next'])
function onLoginClicked() {
    let data = {
        login: department.value.id,
        passwd: password.value
    }
    fetch('/api/pk/login', {
        method: "POST",
        cache: "no-cache",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify(data)
    })
    .then(resp => {
        if(resp.status === 200) {
            emit('next')
        }
        else {
            showAlert.value = true
            password.value = ''
        }
    })
    .catch(e => {
        console.error('Logging:', e)
    })
}

function onTryAgain() {
    showAlert.value = false
}
</script>

<template>
    <div class="container">
        
        <TitleView>
            Logowanie
        </TitleView>

        <template v-if="!showAlert">
            <SelectDepartment v-model="department" />

            <ValidityInputGroup
                v-model="password"
                class="mt-3"
                type="password"
                title="Hasło"
                required
            />

            <LoginButton
                class="mt-5"
                :disabled="!isLoginBtnEnabled"
                @click="onLoginClicked"
            />
        </template>

        <div v-else class="alert alert-danger mt-5">
            <div>Podane dane są niepoprawne!</div>
            <div>Sprawdź czy poprawnie wpisałeś otrzymane hasło.</div>
            <button class="btn btn-lg btn-danger mt-3" @click="onTryAgain">
                Rozumiem, próbujemy jeszcze raz
            </button>
        </div>

    </div>
</template>