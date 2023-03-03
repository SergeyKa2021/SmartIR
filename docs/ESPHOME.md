# How to setup ESPHOME IR remote controller


### ESPHome configuration example
```yaml
esphome:
  name: my_espsmartir
  platform: ESP8266
  board: esp01_1m

api:
  services:
    - service: start_effect
      variables:
        my_brightness: int
        my_effect: string
      then:
        - light.turn_on:
            id: my_light
            brightness: !lambda 'return my_brightness;'
            effect: !lambda 'return my_effect;'
    - service: send_raw_command
      variables:
        enc_proto: string
        command: int[]
      then:
        - remote_transmitter.transmit_raw:
            code: !lambda 'return command;'

remote_transmitter:
  pin: GPIO14
  carrier_duty_percent: 50%
```
