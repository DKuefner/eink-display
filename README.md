# ESPhome Dashboard with Homeassistant
## Using a Lilygo T5 V2.3.1 e-paper Display

My attempt to display PV data from my two solar panels. Data from panels is collect by [openDTU](https://github.com/tbnobody/OpenDTU), then parsed to a Influx DB, visualized via Grafana and node-red.

After this has been done I was looking for a way to display the data on a kind of Display without the need for a permanent power supply. I found this great work by [kotope](https://github.com/kotope/esphome_eink_dashboard/tree/main). The main part of my yaml file is based on this project. However this project is using a 4.7" e-paper Display which wasn't available at the point when I started testing. So I decided for a smaller Display and found the Lilygo T5 V2.3.1. Similarily based on a ESP32 Controller it can be integrated in ESPhome. Some adoptions needed to be done to show data on the samller 2.13" Display. 
### ESP32 deep sleep
To save power and prolongen the battery life the ESP32 deep sleep mode is being used. Due to the small size I decided to display only 3 values, which are yieldtotal, yieldday and power as being delivered by openDTU. Addionaly the date, last update and battery state. The values are being updated every 30 minutes. From 23:00 on the ESP32 sleeps until 6:40 in the morning.

This is the point where I'm looking for a smarter solution, i.e. the ESP32 gets out of sleep mode at sunrise and fall into sleep again at sunset, by keeping the 30 min update interval during the day. Expermenting with the `on_sunset` and `on_sunrise` methods didn't work. It seems that the ESP32 is missing sunset and sunrise events when it's in deep sleep mode at this events.
Currently I'm using fixed row and column values. I'll try to implment X and Y coordinates which seems to b emore flexible.
### Battery and Housing
There are some very nice 3D print housings at Thingiverse like [this](https://www.thingiverse.com/thing:5966664).
For battery I decided for a 750mAh LiPo. Given my current settings it gives a run time of approx. x days.