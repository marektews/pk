<script setup>
const emit = defineEmits(['step'])
</script>

<template>
    <div class="container">
        <div class="card text-bg-dark">
            <div class="card-body">
                <h5 class="card-title">
                    Nowy identyfikator parkingowy
                </h5>
                <h6 class="card-subtitle my-3 text-muted">
                    Wygeneruj identyfikator, aby otrzymać przepustkę 
                    uprawniającą do wjazdu na parking Torwar
                </h6>
                <button 
                    class="btn btn-outline-primary btn-lg" 
                    @click="emit('step', 10)"
                >
                    Wygeneruj
                </button>
            </div>
        </div>

        <div class="card text-bg-dark mt-3">
            <div class="card-body">
                <h5 class="card-title">
                    Aktualizacja identyfikatora parkingowego
                </h5>
                <h6 class="card-subtitle my-3 text-muted">
                    Jeśli posiadasz już wygenerowany identyfikator i chcesz dokonać zmiany pojazdu
                </h6>
                <button 
                    class="btn btn-outline-primary btn-lg" 
                    @click="emit('step', 20)"
                >
                    Aktualizuj
                </button>
            </div>
        </div>

        <div class="card text-bg-dark mt-3">
            <div class="card-body">
                <h5 class="card-title">
                    Pobieranie identyfikatora parkingowego
                </h5>
                <h6 class="card-subtitle my-3 text-muted">
                    Jeśli posiadasz już wygenerowany identyfikator i chcesz tylko ponownie go pobrać i wydrukować
                </h6>
                <button 
                    class="btn btn-outline-primary btn-lg" 
                    @click="emit('step', 30)"
                >
                    Pobieranie
                </button>
            </div>
        </div>

        <div class="card text-bg-dark mt-3">
            <div class="card-body">
                <h5 class="card-title">
                    Mapa dojazdu
                </h5>
                <h6 class="card-subtitle my-3 text-muted">
                    Mapka pokazuje umiejscowienie wjazdu na parking Torwar.
                </h6>
                <a 
                    href="parking-torwar-mapa.png" 
                    download="parking-torwar-mapa.png" 
                    class="btn btn-lg btn-outline-primary"
                >
                    Pobierz mapę
                </a>
            </div>
        </div>        
    </div>
</template>