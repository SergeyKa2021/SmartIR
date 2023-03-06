# How to setup ESPHOME IR remote controller


### ESPHome configuration example
```yaml
esphome:
  name: my_espsmartir
  platform: ESP8266
  board: esp01_1m

api:
  services:
    - service: send_ir_command
      id: ir_trx
      variables:
        ir_address: int
        ir_command: int
        ir_enc_protocol: string
        ir_pronto_data: string
        ir_raw_code: int[] 
      then:
        - if:
            condition:
              lambda: 'return ir_enc_protocol == "Panasonic";'
            then:
              - remote_transmitter.transmit_panasonic
                address: !lambda 'return ir_address;' 
                command: !lambda 'return ir_command;' 
            else: 
      
remote_transmitter:
  pin: GPIO14
  carrier_duty_percent: 50%
```

