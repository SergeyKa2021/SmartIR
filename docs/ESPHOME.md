# How to setup ESPHOME IR remote controller


### ESPHome configuration example
```yaml
esphome:
  name: my_espsmartir
  platform: ESP8266
  board: esp01_1m

api:
  services:

# Service for Panasonic remote
    - service: send_ir_panasonic
      variables:
        ir_address: int
        ir_command: int
      then:
        - remote_transmitter.transmit_panasonic:
            address: !lambda 'return ir_address;' 
            command: !lambda 'return ir_command;' 

# Service for Raw remote
    - service: send_ir_raw
      variables:
        ir_raw_code: int[]
      then:
        - remote_transmitter.transmit_raw:
            code: !lambda 'return ir_raw_code;' 
 
# Service for Nec remote
    - service: send_ir_nec
      variables:
        ir_address: int
        ir_command: int
      then:
        - remote_transmitter.transmit_panasonic:
            address: !lambda 'return ir_address;' 
            command: !lambda 'return ir_command;' 

#       ir_pronto_data: string
      

remote_transmitter:
  pin: GPIO14
  carrier_duty_percent: 50%
```

