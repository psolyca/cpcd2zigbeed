<div align="center">
<h1>
Home Assistant Community App for<br>
RCP firmware of RTL8196E Gateway — Open Linux Firmware 
</h1>

This app for Home Assistant provide the Zigbee — EmberZNet 8.2.2 / EZSP 18 stack to connect [Zigbee2MQTT](https://www.zigbee2mqtt.io/guide/usage/integrations/home_assistant.html)
to your [RTL8196E gateway](https://github.com/jnilo1/rtl8196e-gateway/tree/main) (Lidl Silvercrest, Sengled G4) with the **RCP firmware**.<br>
</div>

App available for :  
![Supports aarch64 Architecture][aarch64-shield]
![Supports amd64 Architecture][amd64-shield]  

Based on cpcd-zigbeed image from [RTL8196E Gateway](https://github.com/jnilo1/rtl8196e-gateway).  

## Install firmware

If you did not have it, **[flash the Open Source firmware first](https://github.com/jnilo1/rtl8196e-gateway/tree/main)**.  
Then follow **only [step 1 to flash the RCP firmware](https://github.com/jnilo1/rtl8196e-gateway/tree/main/2-Zigbee-Radio-Silabs-EFR32/25-RCP-UART-HW#step-1--flash-the-rcp-firmware)**.  

## Install App
Add this repository by going to the **App Store** panel, click **⋮ → Repositories**, fill in `https://github.com/psolyca/cpcd2zigbeed` and click **Add → Close**.  
Install the app in the **App Store**  
  
Or click the button below, click **Add → Close** (You might need to enter the **internal IP address** of your Home Assistant instance first).  
[![Open your Home Assistant instance and show the app store with a specific repository URL pre-filled.](https://my.home-assistant.io/badges/supervisor_store.svg)](https://my.home-assistant.io/redirect/supervisor_store/?repository_url=https%3A%2F%2Fgithub.com%2Fpsolyca%2Fcpcd2zigbeed)  

## Configure app
In the **configuration** tab of **CPCd2Zigbeed** app fill **RTL8196E Gateway IP**.  

In the **configuration** tab of **Zigbee2MQTT** app set the serial section to point at this app, using the IP address of your Home Assistant host:

```yaml
serial:
  port: tcp://<home-assistant-ip>:9999
  adapter: ember
```

zigbeed accepts a single client at a time: connect either Zigbee2MQTT or ZHA, not both.

The Zigbee network state (`host_token.nvm`) is stored in the app's `/data` directory and is kept across restarts and updates.  


[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg