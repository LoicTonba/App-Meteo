<template>
    <div class="container">
        <h1 class="my-4">App météo avec Vue.js 2.6.14</h1>
        <div class="form-groupe mb-5">
            <label for="position" class="mb-2">Entrez le nom d'une ville</label>
            <input 
            id="position" 
            type="text" 
            class="form-control"
            v-model="requete"
            @keypress.enter="goMeteo">
        </div>

        <div class="w-75 m-auto" v-if="temps">
            <h3 class="text-center mb-3">Position:
                {{ temps.name }}
            </h3>
            <div class="card text-center p-5">
                <p class="texte-affichage">
                    Temperature : {{ temps.main.temp.toFixed() }}
                </p>
                <p class="texte-affichage">
                    Temps : {{ temps.weather[0].description }}
                </p>
            </div>
        </div>
        <p class="copy mb-10" v-if="temps">copyright &copy; 2024 TONBA LOIC</p>
    </div>    
</template>

<script>

import axios from 'axios'
export default {
    name:'Me_teo',
    data(){
        return {
            requete:'',
            temps: undefined,
            api_code:'e065a5ef8a87915a0d040fb9b50bcca7', 
            url_recherche:'https://api.openweathermap.org/data/2.5/weather?'
        }
    },
    methods: {
        goMeteo(){
            

                axios
                .get(`${this.url_recherche}q=${this.requete}&
                units=metric&APPID=${this.api_code}&lang=fr`)
                .then(reponse => {
                    //console.log(reponse);
                    this.temps = reponse.data;
                    console.log(this.temps)
                })
                this.requete = ''
            
        }
    }
}
</script>

<style scoped>
.texte-affichage{
    font-size: 40px;
    font-weight: 300;
    line-height: 1.2;
}
.copy{
    text-align: center;
    bottom: 50px;
}

</style>
