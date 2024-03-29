# Homebridge Plugin for LG 2012 Series TVs

This fork for:  Specific for for a LG55LM760-ZB. (Old TV) 
 To Do, fix volume control from the native ios remote
 To Do, fix or confirm On/Off power cycle control from homekit home app

Homebridge Plugin based off (https://npmjs.org/package/homebridge-lgtv2) to allow Siri to control LGTV 2012 series.

Hacked together to work with the native IOS 10 Home App, the plugin emulates a light bulb, and maps the brightness control to volume.

## Features
* Power on/off (Works with IOS Home App) 

* Change volume (Works with IOS Home App)
The Brightness (Volume) is controlled by percentage, according to the max_volume parameter. My TV can go to 50, but this seems way to loud: so the default is 20.
A min_volume parameter mutes the tv when the volume is lowered. to try and prevent homekit setting power to 0, as its current behaviour


## Very Experimental
* Channel + Volume Control
This is possible using the hue control in the [Elgato Eve](https://www.elgato.com/en/eve/eve-app) app.

Setting "false_run" to true in the config can trys prevent the channel changes whilst experimenting with this


## Install
```
npm install -g homebridge-lgtv-2012
```

## Get TV Pairing key
Replacing 172.16.0.10 with your TV's ip
```
cd $NODE_PATH/homebridge-lgtv-2012
node -e "ip = '172.16.0.10'; lg = require('lgtv-2012').lgtv; tv = new lg({host: ip}); tv.pair_request()"
```

## Configuration example
```json
{
  "accessories": [
    {
      "accessory": "lgtv-2012",
      "name": "TV",
      "ip": "10.0.1.4",
      "pairingKey": "123456",
      "min_volume": 2, "max_volume": 20,
      "on_command": "MUTE"
    }
  ]
}
```

### Configuration fields

- `accessory` [required]
Must always be lgtv-2012
- `name` [required]
Name of your accessory
- `ip` [required]
IP address of your tv
- `pairingKey` [required]
Must be provided to control the TV. If not provided, pairing key should be shown on the tv during accessory setup.
- `max_volume` [optional]
Upper Volume Limit (default: 20)
- `min_volume` [optional]
Lower Volume Limit before muting the TV (default: 2)
- `on_command` [optional]
Wake-on-Lan is not supported, so command to send when siri is asked to "Turn TV on" (default: "MUTE")
