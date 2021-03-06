---
title: Introduction
---
 
  <div class="max-w-screen-xl mx-auto pb-5">
    <div class="p-2 rounded-lg bg-indigo-100 shadow-lg sm:p-3">
    <div class="flex items-center">
          <span class="p-2 rounded-lg bg-indigo-500">
            <svg class="h-8 w-8 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5.882V19.24a1.76 1.76 0 01-3.417.592l-2.147-6.15M18 13a3 3 0 100-6M5.436 13.683A4.001 4.001 0 017 6h1.832c4.1 0 7.625-1.234 9.168-3v14c-1.543-1.766-5.067-3-9.168-3H7a3.988 3.988 0 01-1.564-.317z" />
            </svg>
          </span>
        <div class="flex-wrap flex">
          <p class="pt-1 text-indigo-700 font-medium">
              Ha艂as jest w fazie beta. Wy艣lij pytania do</p></p>
        <a href="mailto:Noise@Sensor.Community" class="ml-1 font-medium underline text-white hover:text-yellow-600">
                Noise@Sensor.Community</a>
        </div>
    </div>
  </div>
</div>


> 馃毀 Zbuduj sw贸j czujnik DIYY i sta艅 si臋 cz臋艣ci膮 艣wiatowej sieci opendata i civictech. Dzi臋ki DNMS (Digital Noise Measuring Sensor) mo偶esz samodzielnie mierzy膰 poziom ha艂asu.

 <img src="../docs/dnms/dnms-noise-measuring-sensor-kit.jpg" style="display: block; margin: 1em 0" loading="lazy"/>


Sprawd藕 oryginalne instrukcje i poprzednie wersje czujnika ha艂asu na [Helmut Bitter's Github](https://github.com/hbitter/DNMS/tree/master/Manual).

<br>

To repozytorium zawiera r贸偶ne konfiguracje do budowy czujnika z r贸偶nych rodzaj贸w p艂ytek i p艂ytek drukowanych.
 
 <br>
 
 Istniej膮 dwa r贸偶ne rodzaje ustawie艅:
 
* konfiguracja, w kt贸rej NodeMCU z niekt贸rymi czujnikami (PM, temperatura itp.) i DNMS s膮 rozdzielone. P艂ytki drukowane nazywaj膮 si臋 AIRROHR V1.4 a DNMS - T4 V1.4.
* po艂膮czona wersja NodeMCU i DNMS na tej samej p艂ytce PCB: DNMS - T4+NodeMCU V1.4
  
 Opisany jest tu tylko wariant, w kt贸rym NODEMCU i DNMS s膮 rozdzielone. Sp贸jrz na Helmut's Github dla pozosta艂ych wariant贸w!
 
  W tym przypadku po艂膮czenie pomi臋dzy NodeMCU i DNMS mo偶e mie膰 d艂ugo艣膰 nawet 10 m. Jest to wa偶ne, poniewa偶 nale偶y znale藕膰 odpowiednie po艂o偶enie DNMS, aby uzyska膰 dok艂adne pomiary ha艂asu.

### Lista zakup贸w

##### Pojedyncze komponenty
* [NodeMCU ESP8266 CPU/WLAN](https://www.aliexpress.com/wholesale?groupsort=1&SortType=price_asc&SearchText=nodemcu+v3+esp8266+ch340)
* [Teensy 4.0 development board](https://www.pjrc.com/store/teensy40.html). Inni sprzedawcy: [EXPTECH](https://www.exp-tech.de/plattformen/teensy/9596/teensy-4.0-development-board), [Antratek](https://www.antratek.de/teensy-4-0), [PIMORONI](https://shop.pimoroni.com/products/teensy-4-0-development-board)
* [Digitales Mikrofon ICS-43434](https://www.tindie.com/products/onehorse/ics43434-i2s-digital-microphone/)
* ultra elastyczne kable silikonowe o 艣rednicy 0,15 mm虏 (AWG 26) w 6 r贸偶nych kolorach
<br>
Czujnik DNMS (Digital Noise Measuring Sensor) mo偶e by膰 po艂膮czony z czujnikiem PM AirRohr:

* [SPS30 Czujnik drobnego py艂u](https://www.sparkfun.com/products/15103).  Inni sprzedawcy: [TME](https://www.tme.eu/de/details/sps30/gassensoren/sensirion/1-101638-10/?brutto=1), [SOS electronic](https://www.soselectronic.de/products/sensirion/sps30-2-304234). Mo偶na r贸wnie偶 zastosowa膰 zwyk艂y czujnik [SDS011 PM sensor](https://de.aliexpress.com/wholesale?catId=0&initiative_id=AS_20200813122806&SearchText=sds011) can be used as well.
* [BME280 6-PIN Version, temperatura i wilgotno艣膰](https://www.aliexpress.com/wholesale?catId=0&initiative_id=SB_20200308040440&SearchText=bme280+-5V+%2B3.3V). Inni sprzedawcy: [Nettigo](https://nettigo.eu/products/module-pressure-humidity-and-temperature-sensor-bosch-bme280), [Berrybase](https://www.berrybase.de/bauelemente/sensoren-module/feuchtigkeit/bme680-breakout-board-4in1-sensor-f-252-r-temperatur-luftfeuchtigkeit-luftdruck-und-luftg-252-t)
* [Przew贸d](http://www.aliexpress.com/wholesale?groupsort=1&SortType=price_asc&SearchText=Dupont+cable+20cm+female-female)
* [Przew贸d USB np.: p艂aski 2m Micro-USB](https://www.aliexpress.com/wholesale?catId=0&initiative_id=SB_20200308040708&SearchText=micro+usb+flat+cable+2m)
* [Zasilacz USB](https://www.aliexpress.com/wholesale?catId=0&initiative_id=SB_20200308040834&SearchText=single+micro+usb+eu+power+supply)
* [Ta艣my kablowe](https://www.aliexpress.com/wholesale?catId=0&initiative_id=SB_20200308040852&SearchText=cable+straps)

Poni偶ej opisane zostan膮 p艂ytki drukowane i ochrona przed warunkami atmosferycznymi.

<br>

馃檶 艢wietnie, zdecydowa艂e艣 si臋 na zakup cz臋艣ci online! 
Niestety dostawa mo偶e trwa膰 od dni do trzech tygodni. 
Do tego czasu mo偶na korzysta膰 z witryny life锔?.
