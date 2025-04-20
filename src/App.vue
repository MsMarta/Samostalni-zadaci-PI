<script setup>
import { ref } from 'vue'

const korisnik = ref ({
    jeAdmin: true,
    osobni_podaci: {
        ime: "Marko",
        prezime: "Krivić",
        adresa: {
            grad: "Pula",
            ulica: "Veruda",
            broj: 32
        },
        broj_telefona: "+091-123-456"
    },
    kosarica: [
        { naziv: "Jabuka", količina: 4 },
        { naziv: "Mrkva", količina: 12 },
        { naziv: "Sir", količina: 1 },
        { naziv: "Kruh", količina: 3 },
    ]
})
 
const slike= ref({
    "Jabuka": "https://www.svgrepo.com/show/530203/apple.svg",
    "Mrkva": "https://www.svgrepo.com/show/530216/carrot.svg",
    "Sir": "https://www.svgrepo.com/show/530219/cake.svg",
    "Kruh": "https://www.svgrepo.com/show/530223/bread.svg",
})

const proizvodi = ref ([
    { naziv: "Jabuka", cijena: 0.25 },
    { naziv: "Mrkva", cijena: 0.12 },
    { naziv: "Kruh", cijena: 2.00 },
    { naziv: "Sir", cijena: 4.48 }
])

function dohvatiCijenu(naziv) {
  const proizvod = proizvodi.value.find(p => p.naziv === naziv)
  return proizvod ? proizvod.cijena : 0
}

function sveukupnaCijena() {
  let ukupno=0
  for (let i of korisnik.value.kosarica){
    ukupno+= (dohvatiCijenu(i.naziv))*i.količina
  }
  return ukupno
}

function najskupljaStavka() {
  let najskuplja=""
  let najvecaCijena=0
   
  for (let i of korisnik.value.kosarica){
    let ukupno= (dohvatiCijenu(i.naziv))*i.količina

  if (ukupno > najvecaCijena){
    najvecaCijena=ukupno
    najskuplja=i.naziv
  }

  }
  return najskuplja
}
</script>

<template>
  <br>
<div class="kosarica" :style="{ color: korisnik.jeAdmin ? 'blue' : 'black' }">
  <h2>Korisnički podaci</h2>
  <hr>
  <p>Ime: {{ korisnik.osobni_podaci.ime }}</p>
  <p>Prezime: {{ korisnik.osobni_podaci.prezime }}</p>
  <p>Adresa: {{ korisnik.osobni_podaci.adresa.ulica }} {{ korisnik.osobni_podaci.adresa.broj }} , {{ korisnik.osobni_podaci.adresa.grad }}</p>
  <p>Telefon: {{ korisnik.osobni_podaci.broj_telefona }}</p>
</div>
<br>
<div class="stavke">
  <h2>Košarica</h2>
  <ul> 
    <li class="lista" :style="{ color: korisnik.kosarica[0].naziv === najskupljaStavka() ? 'red' : 'white' }">
    <img src="https://www.svgrepo.com/show/530203/apple.svg" width="50" alt="test-slika" /> <br>
    {{ korisnik.kosarica[0].naziv }} <br>
    Količina: {{ korisnik.kosarica[0].količina }} | Cijena: {{ proizvodi[0].cijena }} <br>
    Ukupno: € {{ dohvatiCijenu("Jabuka") * korisnik.kosarica[0].količina }}
    </li>
    <br>
    <li class="lista" :style="{ color: korisnik.kosarica[1].naziv === najskupljaStavka() ? 'red' : 'white' }">
    <img src="https://www.svgrepo.com/show/530216/carrot.svg" width="50" alt="test-slika" /> <br>
    {{ korisnik.kosarica[1].naziv }} <br>
    Količina: {{ korisnik.kosarica[1].količina }} | Cijena: {{ proizvodi[1].cijena }} <br>
    Ukupno: € {{ dohvatiCijenu("Mrkva") * korisnik.kosarica[1].količina }}
    </li>
    <br>
    <li class="lista" :style="{ color: korisnik.kosarica[2].naziv === najskupljaStavka() ? 'red' : 'white' }">
    <img src="https://www.svgrepo.com/show/530219/cake.svg" width="50" alt="test-slika" /> <br>
    {{ korisnik.kosarica[2].naziv }} <br>
    Količina: {{ korisnik.kosarica[2].količina }} | Cijena: {{ proizvodi[3].cijena }} <br>
    Ukupno: € {{ dohvatiCijenu("Sir") * korisnik.kosarica[2].količina }}
    </li>
    <br>
    <li class="lista" :style="{ color: korisnik.kosarica[3].naziv === najskupljaStavka() ? 'red' : 'white' }">
    <img src="https://www.svgrepo.com/show/530223/bread.svg" width="50" alt="test-slika" /> <br>
    {{ korisnik.kosarica[3].naziv }} <br>
    Količina: {{ korisnik.kosarica[3].količina }} | Cijena: {{ proizvodi[2].cijena }} <br>
    Ukupno: € {{ dohvatiCijenu("Kruh") * korisnik.kosarica[3].količina }}
    </li>
    <p style="text-align: center;"><b>Ukupna cijena: € {{ sveukupnaCijena() }} </b></p>
  </ul>
</div>
<br>
<br>
</template>

<style scoped>
.kosarica{
  background-color: rgb(240, 207, 245);
  border: 3px solid black;
  width: 30%;
  margin: auto;
  padding: 10px;
  border-radius: 30px;

}

.stavke{
  background-color: rgb(240, 207, 245);
  border: 3px solid black;
  width: 30%;
  margin: auto;
  padding: 10px;
  border-radius: 30px;
}

.lista{
border: 2px solid black;
background-color: rgb(107, 61, 110);
padding: 5px;
}

ul{
  list-style-type: none;
  padding: 0;
  margin: 0;
}
</style>
