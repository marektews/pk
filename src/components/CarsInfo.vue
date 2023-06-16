<template>
    <div class="mt-3 alert alert-info alert-layout">
        <i class="fa-solid fa-circle-info" />
        <ol>
            <li>Identyfikator uprawnia do wjazdu na parking tylko jeden pojazd danego dnia.</li>
            <li>Można na jeden identyfikator zgłosić wjazd różnych pojazdów, ale tylko w różne dni.</li>
        </ol>
    </div>
</template>

<style scoped>
.alert-layout {
    display: flex;
    flex-direction: row;
    align-items: first baseline;
    gap: 6pt;
}

ol {
    margin-bottom: 0;
}
</style>