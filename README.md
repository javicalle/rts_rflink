# RTS_RFLink
After trying some of the time controlled covers based in automations (with poor results) I found the implementation for KNX cover:
* https://github.com/home-assistant/home-assistant/blob/dev/homeassistant/components/knx/cover.py 99

This piece of code is the basis for my implementation. The merit and all my grats for the KNX developers/mainteners.

My implementation extends RFLinkCover and is very specific for RTS covers (a.k.a. Somfy covers).

It works better with `wait_for_ack: false` (disabled).

```
# RFLink component
rflink:
  port: /dev/serial/by-id/usb-1234_USB2.0-Serial-abcd-port0
  wait_for_ack: false
```

If not setted, every command can take up to 4 seconds to execute and some commands can get lost, executed when cover is stoped or whatever.

You must configure the travel times (in seconds) and the MY position (0-100 where 0 is closed and 100 open). The MY position is used to calculate the cover position.

```yaml
  - platform: rts_rflink
    devices:
      RTS_0A8720_0:
        name: enanos
        rts_my_position: 10
        travelling_time_down: 14
        travelling_time_up: 15
        aliases:
          - rts_31e53f_01
          - rts_32e53f_01
          - RTS_32E542_0
```
