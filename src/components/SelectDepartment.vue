<script setup>
import { ref, computed, onMounted } from 'vue'

const hints = ref([])
const selected = computed({
    get() {
        return props.modelValue
    },
    set(value) {
        emit('update:modelValue', value)
    }
})
const onelang = computed(() => {
    let o = {}
    hints.value.forEach(element => {
        o[element] = 1
    });
    return Object.keys(o).length === 1
})

const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue', 'finished'])

onMounted(async () => await getHints())

async function getHints() {
    try {
        const res = await fetch(`/api/pk/hints`)
        if(res.status === 200) {
            hints.value = await res.json()
        }
    }
    catch(e) {
        console.debug(e)
    }
}
</script>

<template>
    <div>
        <label class="form-label">
            Nazwa działu kongresowego
        </label>

        <select 
            v-model="selected"
            class="form-select form-select-lg"
        >
            <option v-for="(item, index) in hints" :key="index" :value="item">
                <span v-if="onelang">
                    {{ item.name }}
                </span>
                <span v-else>
                    {{ item.lang }} - {{ item.name }}
                </span>
            </option>
        </select>
    </div>
</template>