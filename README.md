# minihass_ext
Extensions I made for Fredrik's [minihass](https://github.com/fredrikpersson92/minihass/)


## Setting up garbage collection

I have four sensors for the type of garbage and the days with the minimal days across all types when collection is scheduled.
![](/pictures/garbage_collection.gif)

The dashboard part is here:

```yaml
  - type: "custom:button-card"
    template:
      - custom_card_garbage_collection
    variables:
      label: Days until next<br>collection
      counter: >
        [[[ return states['sensor.gcoll_next_date'].attributes.days ]]]
      hausmuell: >
        [[[ return states['sensor.hausmuell_alert'].state ]]]
      paper: >
        [[[ return states['sensor.paper_alert'].state ]]]
      bio: >
        [[[ return states['sensor.bio_alert'].state ]]]
      gelbersack: >
        [[[ return states['sensor.gelbersack_alert'].state ]]]
    entity: input_boolean.toggle_button_notify_garbage
```

The code for the extension of Fredrik's version can be found [here](https://) 

## Setting up irrigation piece

For the irrigation control of my four hunter valves I am using Robert Cook's implementation [irrigation unlimited](https://github.com/rgc99/irrigation_unlimited).

The cards of my dashboard are basically two:

![](/pictures/irrigation_animation.gif)

The right card contains the valve entity and a runtime, that can be set, including a progress bar, that shows up, when triggered.
The left card is the controller card, that initiates the manual run. The card can enable the valve by switching a toggle.

Only, when enabled the manual service can be fired. The card then blinks "with ease" ;-) and the right valve card shows the progress of irrigation.

My dashboard piece is as follows:

```yaml
  # example for Zone 1
  - type: horizontal-stack
    cards:
      - type: "custom:button-card"
        template:
          <b>- custom_card_manual</b>
        variables:
          name: Manuell
          zone_name: "Z1: Hinten links"
          background: "var(--gradient-blue)"
          timer: input_datetime.irrigation_timer_z1
        entity: binary_sensor.irrigation_unlimited_c2_z1

      - type: "custom:button-card"
        template:
          - custom_card_irrigation_new
        variables:
          name: Beregnung
          zone_name: "Z1: Hinten links"
          background: "var(--gradient-green)"
          timer: input_datetime.irrigation_timer_z1
        entity: binary_sensor.irrigation_unlimited_c2_z1
```
