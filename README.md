# HASS_pws_scraper
HomeAssistant scraper for weather station based on ObserverIP box (es. FineOffset, Ambient Weather, Aercus etc).


This is a very slightly modified version of the Multiscrape custom_component from @danieldotnl.
You can find he's works here: https://github.com/danieldotnl/hass-multiscrape

I edited the name of the plugin, so you can have both running on the same Hass instance.

For using this componente download and copy the pws_scrape folder inside your custom_component folder and restart HomeAssistant.
Later add the value of the sensor you want in configuration.yaml, for example:

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
        
        
You can add also the other element you see in the livedata.html page of the ObserverIP, just add other "selectors" as above adapting the select element number
