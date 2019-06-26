# geo_address
===============
A plugins to automatically lookup address information from device position.

The plugins will create new state information named after the existing device_trackers in Homeassistant.

<img src="docs/device_trackers.png" alt="Device trackers"/>

## Usage
Add this to configuration.yaml

```yaml
geo_address:
  update_interval: 60
  update_period: 3600
  use_state: true
```

| property | Example | Result
| ------------ | ------- | ------
| update_interval | `60` | how often to check for new position
| update_period | `3600` | for how long back in time to check for changes
| use_state | `true` | use state change updates




Example implementation in Lovelace. I've used Thomas Lovéns Lovelace module <a href="https://github.com/thomasloven/lovelace-markdown-mod">lovelace-markdown-mod</a> for this. 
```yaml
type: markdown
  content: >
    [[ geo_address.samsung9.attributes.road ]] [[ if(geo_address.samsung9.attributes.house_number != undefined, geo_address.samsung9.attributes.house_number, "") ]]
    [[ if(geo_address.samsung9.attributes.city != undefined, geo_address.samsung9.attributes.city, "") ]] 
```


