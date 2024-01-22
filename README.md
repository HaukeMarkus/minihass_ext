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

The card I made is for manually starting an irrigation per zone.
The card contains the name of the valve you like it to display, a toggle switch enabling or disabling the valve and a duration slider.
When tapping the whole card **and** with the toggle switch **enabled**, then the irrgation starts showing a countdown progress slider.

![](/pictures/an_irrigation_cards.gif)

The code of the card can be found [here](https://github.com/HaukeMarkus/minihass_ext/blob/main/custom_cards/custom_card_irrigation/custom_card_manual.yaml)

My dashboard piece is as follows:

```yaml
  # Zone 1
  # - type: horizontal-stack
  #   cards:
  - type: "custom:button-card"
    template:
      - custom_card_manual
    variables:
      name: Manuelle Beregnung
      zone_name: Hinten links
      background: var(--gradient-blue)
      entity_timer: input_number.zone1_min
      entity_timerval: sensor.iu_timer_z1
    entity: binary_sensor.irrigation_unlimited_c2_z1

```

## Setting up a window-shuttor card

For the controlling my shutters I made a card based on the minimalist cover card. 
Mine only considers showing basic info and basic controlling:

A sample of it...:

![](/pictures/shutters.png)

Using it in your dashboard:

```yaml
  # Front shutters
  - type: "custom:button-card"
    template:
      - custom_card_section_title
    variables:
      section_title: Front

  - type: horizontal-stack
    cards:
      - type: "custom:button-card"
        template:
          - custom_card_cover
        entity: cover.rolladen_bad
        variables:
          cover_name: Klo
```
