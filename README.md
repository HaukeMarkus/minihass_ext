# minihass_ext
Extensions I made for minihass


## Setting up garbage collection

I have four sensors for the type of garbage and the days with the minimal days across all types when collection is scheduled.
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
