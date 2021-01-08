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
    resource: 'http://192.168.99.65/livedata.htm'
    selectors:
      temp_outdoor:
        name: Outdoor Temperature
        select: "tr:nth-of-type(11) input"
        unit_of_measurement: '°C'
      humidity_outdoor:
        name: Outdoor Humidity
        select: "tr:nth-of-type(12) input"
        unit_of_measurement: '%'
      wind_direction:
        name: Wind Direction
        select: "tr:nth-of-type(13) input"
      wind_avgspeed:
        name: Averange Wind Speed
        select: "tr:nth-of-type(14) input"
        unit_of_measurement: 'km/h'
      wind_gustspeed:
        name: Gust Wind Speed
        select: "tr:nth-of-type(15) input"
        unit_of_measurement: 'km/h'
      solar_radiation:
        name: Solar Radiation
        select: "tr:nth-of-type(17) input"
        unit_of_measurement: 'w/m2'
      rain_rate:
        name: Rain Gauge
        select: "tr:nth-of-type(21) input"
        unit_of_measurement: 'mm/h'
      rain_event:
        name: Precipitation
        select: "tr:nth-of-type(22) input"
        unit_of_measurement: 'mm/h'
```    

You can add also the other element you see in the livedata.html page of the ObserverIP, just add other "selectors" as above adapting the select element number.

You can customize the icon related to the sensors created by the customize.yaml file, or trough the webgui Configuration -> Customizations. Here mine:


```yaml
customize.yaml

sensor.rain_rate:
  icon: mdi:weather-pouring
sensor.rain_event:
  icon: mdi:weather-rainy
sensor.wind_avgspeed:
  icon: mdi:weather-windy
sensor.wind_gustspeed:
  icon: mdi:weather-windy
sensor.wind_direction:
  icon: mdi:compass
sensor.solar_radiation:
  icon: mdi:white-balance-sunny
sensor.humidity_outdoor:
  icon: mdi:water
```   
