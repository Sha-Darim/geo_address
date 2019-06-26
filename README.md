# geo_address
A plugin to automatically lookup address information using device_tracker position.

The plugins will create new state information named after the existing device_trackers in Homeassistant.

The plugin uses device trackers<br/>
<img src="docs/device_trackers.png" alt="Device trackers"/>

...to create address info<br/>
<img src="docs/geo_address.png" alt="geo_address"/>


The plugins uses Nominatim from geopy.geocoder as the base for the reverse lookups.


## Usage


Add this to `configuration.yaml`

```yaml
geo_address:
  update_interval: 60
  update_period: 3600
  use_state: true
```

| property | Example | Result
| ------------ | ------- | ------
| use_timed | `true` | use timed updates
| use_state | `true` | use state change updates
| update_interval | `60` | how often to check for new position
| update_period | `3600` | for how long back in time to check for changes



## Implementation
Example implementation in Lovelace. I've used Thomas Lovéns Lovelace module <a href="https://github.com/thomasloven/lovelace-markdown-mod">lovelace-markdown-mod</a> for this. 
```yaml
type: markdown
  content: >
    <h3>Adress</h3>
    [[ geo_address.fredric_fredric.attributes.road ]] [[ if(geo_address.fredric_fredric.attributes.house_number != undefined, geo_address.fredric_fredric.attributes.house_number, "") ]]
    [[ geo_address.fredric_fredric.attributes.city ]] 
```

<img src="docs/address_card.png" alt="Address card"/>

## Example usage
<img src="docs/example.png" alt="Fredric address"/>
Standard picture entity card and markdown below. 

```yaml
    - type: "custom:vertical-stack-in-card"
      cards:
      - type: vertical-stack
        cards:
          - type: picture-entity
            entity: device_tracker.fredric_fredric
            image: /local/lovelace/Fredric.jpg
            show_name: false
          - type: markdown
            content: >
              <h3>Adress</h3>
              [[ geo_address.fredric_fredric.attributes.road ]] [[ if(geo_address.fredric_fredric.attributes.house_number != undefined, geo_address.fredric_fredric.attributes.house_number, "") ]]
              [[ if(geo_address.fredric_fredric.attributes.city != undefined, geo_address.fredric_fredric.attributes.city, "") ]]
              [[ if(geo_address.fredric_fredric.attributes.village != undefined, geo_address.fredric_fredric.attributes.village, "") ]]
              [[ if(geo_address.fredric_fredric.attributes.county != geo_address.fredric_fredric.attributes.city, geo_address.fredric_fredric.attributes.county, "") ]]  
```

In the screen dump above. I've used <a href="https://github.com/custom-cards/vertical-stack-in-card">vertical-stack-in-card</a> to be able to make a tighter fit between the the cards.

## Right now
The are issues left to figure out, like implementing a better way to do state change tracking. The current way isn't good enough and timed updates is probably not the best way to go around this problem. 

Drop a line if you have suggestions or found bugs :-)