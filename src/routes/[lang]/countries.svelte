<script>
    import initI18n from "../../utils/initI18n";
    import { stores } from "@sapper/app";
    import Contact from "../../components/Contact.svelte";
    import * as countries from '../../json/countries.js';
    import {flag} from "country-emoji";
    import Cards from "../../components/Cards.svelte";
//     import * as L from 'leaflet';
//   // If you're playing with this in the Svelte REPL, import the CSS using the
//   // syntax in svelte:head instead. For normal development, this is better.
//     import 'leaflet/dist/leaflet.css';
//     let map;

    const { page } = stores();
    $: lang = $page.params.lang;
    $: i18n = initI18n(lang);

    var countSensor = {};
    // const selector = {};
    const sensorTypes = {"PM":["sds011","sps30","hpm","pms7003"],"noise":["laerm"],"radiation":["radiation_si22g"],"temphumipress":["dht22","bme280"]};

    const today = new Date();
    const yesterday = dateFormater(today);
    console.log(yesterday);
    console.log(countries.array);

    const url_count = 'https://archive.sensor.community/'+ yesterday +'/sensors_per_country.txt';

if (process.browser) {

    fetch(url_count)
    .then(function(response) {
    return response.json();
    })
    .then(function(data) {
        console.log(data[yesterday]);

        // countSensor.PM += data.hpm + data.pms1003 + data.pms3003 + data.pms5003 + data.pms6003 + data.pms7003 + data.sds011 + data.sps30;
        countSensor = data[yesterday];

        document.getElementById('value1').innerHTML = countSensor.sds011.WORLD.toString();
        document.getElementById('value2').innerHTML = countSensor.bme280.WORLD.toString();

    });
};


function selectedCountry(e){ 
    var selection = countries.array.find(obj => {
    return obj.id === e.target.value
    });
    
    if (selection.code != 'WORLD'){
    document.getElementById('map-frame1').src = 'https://stats.sensor.community/sensors_per_country/?simple=yes&country=' + selection.code;
    document.getElementById('map-frame2').src = 'https://'+ selection.id +'.maps.sensor.community/';
    } else {
    document.getElementById('map-frame1').src = 'https://stats.sensor.community/sensors_per_country/';
    document.getElementById('map-frame2').src = 'https://maps.sensor.community/'; 
    }
    
    var PMCount = 0;
    var TRHPCount = 0;
    var radiationCount = 0;
    var noiseCount = 0;

    if (countSensor.sds011.hasOwnProperty(selection.code)){document.getElementById('value1').innerHTML = countSensor.sds011[selection.code].toString()}else{document.getElementById('value1').innerHTML = "0"};
    if (countSensor.bme280.hasOwnProperty(selection.code)){document.getElementById('value2').innerHTML = countSensor.bme280[selection.code].toString()}else{document.getElementById('value2').innerHTML = "0"};

}
    function dateFormater(date) {
    //one day before
     date.setDate(date.getDate()-1);
     var result = date.getUTCFullYear().toString() + "-"+ pad(date.getUTCMonth(),2,true) + "-" + pad(date.getUTCDate(),2,false);
    return result;
}

function pad(num,size,month) {
    if (month == true){
       num += 1;
        num = num.toString();
        }else{
    num = num.toString();
}
    while (num.length < size) num = "0" + num;
    return num;
}




function delaySelector() {
    if (process.browser) {
        setTimeout(function () {
            document.getElementById("countrySelector").addEventListener("change",selectedCountry);
        }, 900);
    }
}



function delayMap1() {
    if (process.browser) {
        setTimeout(function () {
            document.getElementById('map-frame1').src = 'https://stats.sensor.community/sensors_per_country/?simple=yes&country=';
            // document.getElementById("countrySelector").addEventListener("change",selectedCountry);
        }, 900);
    }
}

function delayMap2() {
    if (process.browser) {
        setTimeout(function () {
            document.getElementById('map-frame2').src = 'https://maps.sensor.community/';
        }, 900);
    }
}

</script>

<svelte:head>
    <title>{i18n.t('countries:metaTitle')}</title>

    <meta property="og:title" content={i18n.t('countries:metaTitle')}/>
    <meta property="og:type" content="website"/>
    <meta property="og:url" content=""/>
    <meta property="og:image" content=""/>
</svelte:head>

<section class="container mx-auto mt-10">
    <div class="flex flex-row flex-wrap mt-10 mx-10">
        <div class="w-full flex flex-wrap my-8">
            <div class="w-full text-center md:text-left md:w-1/2">
                <div class="md:w-4/5 md:pr-20 pb-2 pl-0">
                    <h1 class="py-4 md:py-8 md:pb-8 text-4xl md:text-6xl font-black leading-tight">
                        {i18n.t('countries:h1')}</h1>
                </div>
                <p class="text-xl mx-auto md:pr-8 mt-4 mb-4 leading-reading">
                    {i18n.t('countries:description')}️<br>
                </p>
            </div>
            <div class="w-full md:w-1/2 my-12"></div>
        </div>

</section>
    <select id="countrySelector" class="flex" style="height: 2em;" name="country" onLoad="{delaySelector()}">
        {#each countries.array as country}
             <option value="{country.id}">{country.name}</option>
        {/each}
    </select>
    
    <div class="flex" style="height: 5em;">
        <p id="value1" class="text-xl mx-auto md:pr-8 mt-4 mb-4 leading-reading"></p>
        <p class="text-xl mx-auto md:pr-8 mt-4 mb-4 leading-reading">Particulate matter</p>
    </div>

    <div class="flex" style="height: 5em;">
        <p id="value2" class="text-xl mx-auto md:pr-8 mt-4 mb-4 leading-reading"></p>
        <p class="text-xl mx-auto md:pr-8 mt-4 mb-4 leading-reading">Temperature/RH/Pressure</p>
    </div>

    <div class="flex" style="height: 5em;">
        <p id="value3" class="text-xl mx-auto md:pr-8 mt-4 mb-4 leading-reading"></p>
        <p class="text-xl mx-auto md:pr-8 mt-4 mb-4 leading-reading">Radiation</p>
    </div>

    <div class="flex" style="height: 5em;">
        <p id="value4" class="text-xl mx-auto md:pr-8 mt-4 mb-4 leading-reading"></p>
        <p class="text-xl mx-auto md:pr-8 mt-4 mb-4 leading-reading">Noise</p>
    </div>

    <div class="relative z-20 md:block mx-auto md:bg-white md:shadow-lg z-10 mb-10">
        <div class="flex" style="height: 40em;">
            <iframe scrolling="no" class="z-10" id="map-frame1" onLoad="{delayMap1()}"
                    src=""
                    style="width: 45%; height: 95%; margin: auto; "
                    title="sensor.community particulate matter map"></iframe>
             <iframe scrolling="no" class="z-10" id="map-frame2" onLoad="{delayMap2()}"
                    src=""
                    style="width: 45%; height: 95%; margin: auto; "
                    title="sensor.community particulate matter map"></iframe>
        </div>

        <!-- <div class="flex" style="height: 40em;">
           
        </div> -->

    </div>

    <!-- <div class="relative z-20 md:block mx-auto md:bg-white md:shadow-lg z-10 mb-10">
        

    </div> -->
<Contact/>
