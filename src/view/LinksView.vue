<script setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faFilePdf, faFileImage } from '@fortawesome/free-solid-svg-icons';
import BackButton from '@/components/btns/BackButton.vue'

const props = defineProps({
    pkid: { type: String, default: "" },
})

defineEmits(['back'])

function onDownloadPassID() {
    let filename = ''
    fetch(`/api/pk/download/${props.pkid}`)
    .then(response => {
        if(response.status !== 200) return
        const header = response.headers.get('Content-Disposition');
        const parts = header.split(';');
        filename = parts[1].split('=')[1].replaceAll("\"", "");
        console.log('{1} PK download pass card', response, filename)
        return response.blob()
    })
    .then((blob) => {
        let url = window.URL.createObjectURL(blob)
        console.log('{2} PK download pass card', blob, url)
        var a = document.createElement('a');
        a.href = url;
        a.download = filename;
        document.body.appendChild(a);
        a.click();
        a.remove();        
    })
    .catch(err => console.error("PK download pass id error:", err))
}
</script>

<template>
    <div class="container">
        <div class="card text-bg-dark">
            <div class="card-body">
                <h3>Identyfikator</h3>
                <p class="card-text">
                    Wydrukuj ten identyfikator i umieść za przednią szybą samochodu od strony kierowcy.
                    Umiejscowienie identyfikatora powinno ułatwiać jego weryfikację 
                    - przyśpieszy to odprawę przy bramie wjazdowej na parking.
                </p>
                <button 
                    class="btn btn-lg btn-primary" 
                    @click="onDownloadPassID"
                >
                    <FontAwesomeIcon :icon="faFilePdf" />
                    Pobierz identyfikator
                </button>
            </div>
        </div>

        <div class="mt-4 card text-bg-dark">
            <div class="card-body">
                <h3>Mapa dojazdu</h3>
                <p class="card-text">
                    Mapka pokazuje umiejscowienie wjazdu na parking Torwar.
                </p>
                <a
                    href="parking-torwar-mapa.png" 
                    download="parking-torwar-mapa.png" 
                    class="btn btn-lg btn-primary"
                >
                    <FontAwesomeIcon :icon="faFileImage" />
                    Pobierz mapę
                </a>
            </div>
        </div>

        <BackButton 
            class="mt-5" 
            @click="$emit('back')" 
        />
    </div>
</template>