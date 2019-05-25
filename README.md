# HASS-Google-Coral
Local network image processing using the Google Coral USB accelerator stick exposed via a Flask app -> requires [coral-pi-rest-server](https://github.com/robmarkcole/coral-pi-rest-server). The accelerator stick and Home Assistant can be running on different computers as communcation is via the RESTful edndpoints that the Flask app exposes. This code adds an `image processing` entity in Home Assistant whch has a state that is the number of target objects identified in a camera image, e.g an image with 2 people in it will have the state `2`. It will be necessary to experiment with the `confidence` threshold (a percentage, %) that objects are identified at.

Place the `custom_components` folder in your configuration directory (or add its contents to an existing custom_components folder). In your configuration.yaml add:

```yaml
image_processing:
  - platform: google_coral
    ip_address: 192.168.1.107 # the ip of the machine running the flask app
    port: 5000
    confidence: 25 # default 80
    target_object: car # default person
    source:
      - entity_id: camera.local_file
        name: google_coral_car
```

<p align="center">
<img src="https://github.com/robmarkcole/HASS-Google-Coral/blob/master/images/usage_1.png" width="500">
</p>

<p align="center">
<img src="https://github.com/robmarkcole/HASS-Google-Coral/blob/master/images/usage_2.png" width="500">
</p>