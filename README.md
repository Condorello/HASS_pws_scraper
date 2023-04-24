#### Project abandoned. This One Is better:

https://github.com/Condorello/HASS_wu_interceptor

###################


# HASS_pws_scraper
HomeAssistant scraper for weather station based on ObserverIP box (es. FineOffset, Ambient Weather, Aercus etc).


This is a very slightly modified version of the Multiscrape custom_component from @danieldotnl. I've just parsed the retrive datas as pure text in BeautifoulSoup and extract the sensor value inside the script instead from value_template param. Data are refreshed every 60 seconds, lower pooling crash the poor ObserverIP box.
You can find he's works here: https://github.com/danieldotnl/hass-multiscrape

I edited the name of the plugin, so you can have both running on the same Hass instance.

For using this component download and copy the pws_scrape folder inside your custom_component folder and restart HomeAssistant.
Later add the value of the sensor you want in configuration.yaml, for example:


```yaml
configuration.yaml

sensor:
  - platform: pws_scrape
    name: pws_scrape
    resource: 'http://IP_OF_THE_WEATHER_STATION/livedata.htm'
    selectors:
      temp_outdoor:
        name: Temperatura Esterna
        select: "input:nth-child(1)"
        index: 8
        unit_of_measurement: '°C'
      humidity_outdoor:
        name: Umidita Esterna
        select: "input:nth-child(1)"
        index: 9
        unit_of_measurement: '%'
      wind_direction:
        name: Direzione Vento
        select: "input:nth-child(1)"
        index: 10
      wind_avgspeed:
        name: Vento Medio
        select: "input:nth-child(1)"
        index: 11
        unit_of_measurement: 'km/h'
      wind_gustspeed:
        name: Vento Raffica
        select: "input:nth-child(1)"
        index: 12
        unit_of_measurement: 'km/h'
      solar_radiation:
        name: Radiazione Solare
        select: "input:nth-child(1)"
        index: 14
        unit_of_measurement: 'w/m2'
      rain_rate:
        name: Pluviometro
        select: "input:nth-child(1)"
        index: 18
        unit_of_measurement: 'mm/h'
      rain_event:
        name: Precipitazioni
        select: "input:nth-child(1)"
        index: 19
        unit_of_measurement: 'mm/h'
      pws_battery:
        name: Batteria Stazione Meteo
        select: "input:nth-child(2)"
        index: 1
```    

You can add also the other element you see in the livedata.html page of the ObserverIP, just add other "selectors" as above adapting the select element number.

You can customize the icon related to the sensors created by the customize.yaml file, or trough the webgui Configuration -> Customizations. Here mine:


```yaml
customize.yaml

sensor.rain_rate:
  icon: hass:weather-pouring
sensor.rain_event:
  icon: hass:weather-rainy
sensor.wind_avgspeed:
  icon: hass:weather-windy
sensor.wind_gustspeed:
  icon: hass:weather-windy
sensor.wind_direction:
  icon: hass:compass
sensor.solar_radiation:
  icon: hass:white-balance-sunny
sensor.humidity_outdoor:
  icon: hass:water
sensor.pws_battery:
  icon: hass:battery
```   
