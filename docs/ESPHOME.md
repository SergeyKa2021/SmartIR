# How to setup ESPHOME IR remote controller


### Example configuration entry
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
