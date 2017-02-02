## Console 13 Project Page: Bernoulli's Laws

### Subprojects:
   * Boat Game LIDAR Sensors **DONE**

Check out the main page [here](https://TerrenceTran.github.io)

___

**Date:** 18 January 2017 Wednesday

**Objective:** 13a.Boat Game LIDAR Sensors

**Progress Today:** The boat game on this console is a way for the ball to travel from a higher point to a lower point on the game. the boats each have their own linear actuator controlled by a stepper motor. The motion of the boats are supposed to be a fluid back and forth motion to "flow" the ball from one boat to the next till it reaches the bottom position.

![Boat Sensor Holes Front Install](https://lh3.googleusercontent.com/DMsmGsaPRXhLC_WZKXW5EV1qPXhyFqMC_SKo_arEo41XZfSiR-S5nSq_kSEr2_tCdSBVkz2JRU4ol-k4TDYjSMlGeeND_Q2YI0_atuk5EogWHYWB0lDi3Wsl-1YtX4tcxuq60yiMIBKIAgHimPuyVbn7OTJXkTVUyAcWKywdK9BhWyG2MEV_8oLr8onUw1Lm9kFO7g68IH1ApW-vQ5oXun6e_oUKOvTSmZNT8dzAE5M6bSrTSdUFi3xBFpjEk5g-AerIa6hOROW2sAAzpiHwnfwuhq3sa6N-CwQX4qPkrA8PlpCZ9-TY7X2fljs65ASHo3jq9K8QXFtE9POx0gdU_DpBEdZplbNA4X3IDwLWIxXDQFspPwR9qNd0-CIiohZJKaMAo-xs5wGsZhlsuQo_tVG08cGfrZo0I3YcVysxIjRqwRq8W-nskOxw9zXv-e-DYl0eLSofaXCflFL5owuAGOihtv1N0rmEE5D3esona4OVxbsXXZhP_7AWr-FvoHwUUMWqaYq0PpH8q6pkqwg6wRHgeGU2ccIadZryLz7YcyHr0aMXL3hHNc5XeUYw78X8DhoSnAkUuINHNDlMXNR2jKlxYNTCSo5Lmi2jZ2cR8QMHnpFn-0gZ7QbYqcRyU8dfYHGM2ZI-qu71ZR7SSsQGquqGiWDLjJgUXt3Dt9RIYA=w1760-h990-no)

   | The issue with this game comes from ball sensing. Currently, the game has no way of knowing which boat the ball is on if at all. This can cause problems when turning the console on from a dead stop or cause massive delays from autoplaying the game. 

**Challenges:** I was given four of these [LIDAR sensors](https://www.adafruit.com/product/3316) (Light Detection and Ranging) to add to the console. Typically we would use some ball proximity sensors but the ball is too far away and has too much play between the boats for that method to be effective. 

![Adafruit VL6180x](https://lh3.googleusercontent.com/y5y0K77v1rgaMcXd-D31hyOXSSg9JRtv0mHC59rYRPcYilLrpYgTGCv7U9OmSWuwUTD4x6lMSDw8h3HxoCe0MgDqo00ovxIUqieiMTySlNKeh_yvxXZhOueEb4QzHl1_asWlwVHHsKIFIB09IyxsqpcSfa9KN9MDU5m8sRaU59jE2QbKVlngVXulYtAMX6onsaUNerj3TNTJdNq-rNqxN5FIckfYpWUTZE84qUOiYWcXodTukSe7642I-cEaE-KuaL5hb1de3Kkd_55ZX3vUTTrIhKEibezJd1btpVtbeyIxjbIdqOzZfcE3jeDTBjhIrMfv7Gou8TCSJwQ-Jt6qdBbX4agQaQdN3zy2l2_i99M5Q-86SfgTYCmYmJsXzQtd7kEziDnlhyfWnN7kervE3NZMlTpIGPoMp2daNrl7bfTmzQxKMF1VcBaeFIw4d92kSrf-MVfaJOKkVxyd458ZhBrcvwt8rkzrWkQu5Nvuw8e2tFLnB6C8JIYxoQOOXsBb-eGNEnrmaRMqcaz4guTkI4DUR0KkrGEz9Arp5nKHqIhxiPnaXpJiNQXATTj2kETVAPc7z0N3JzvT_RylcKAyIb73Bh_XUbZEjSWkHu01nv3fvwUW_Lda7HVR8c5t31JJ5-rNK_jWSrvCNaPHXvKmpnHPe6trXn9qD7QZdGQa9A=w919-h690-no)

   | These Lidar sensors are a bit of a challenge to use. Unlike our normal sensor interface [PWR, GND, SIGNAL], these LIDAR sensors interface through the I2C serial bus. As such, they will not work with arduino's inbuilt *digitalRead* functions and need some TLC to mate properly with the game. 

Today was spent testing out one of the sensors and getting familiar with programing one of them. After downloading the [Adafruit library](https://github.com/adafruit/Adafruit_VL6180X), I used the avaliable example code to run the sensor.

```cpp
// Single driver for vl6180x LIDAR sensor. Only 1 sensor can be hooked up directly to the I2C bus

#include <Wire.h>
#include "Adafruit_VL6180X.h"

Adafruit_VL6180X vl = Adafruit_VL6180X();

void setup() {
  Serial.begin(115200);

  // wait for serial port to open on native usb devices
  while (!Serial) {
    delay(1);
  }
  
  Serial.println("Adafruit VL6180x test!");
  if (! vl.begin()) {
    Serial.println("Failed to find sensor");
    while (1);
  }
  Serial.println("Sensor found!");
}

void loop() {
  //float lux = vl.readLux(VL6180X_ALS_GAIN_5);

  //Serial.print("Lux: "); Serial.println(lux);
  
  uint8_t range = vl.readRange();
  uint8_t status = vl.readRangeStatus();

```

   |Most of the setup is taken care of via the library. You really just define the libraies, hit begin and start reading. 

The values that came out are pretty consistant. The sensor is really good at tracking objects but it gets spotty when new object jump into its line of sight and if the ambient light is inconsistent. Still, the differences detected are defined enough for me to have conidence that we can make them work in our system. After a sensor is triggered on a boat, it really doesn't need to be usead again during the same game. Aslong as its trigger right once, we'll be golden.

**Moving Forward:** Tomoorrow I'll try putting multiple sensors together and reading all of their values simultaneously.

___

**Date:** 19 January 2017 Thursday

**Objective:** 13a.Boat Game LIDAR sensors

**Progress Today:** Early morning we got snagged on this breaking issue, there is not in inbuilt method of adressing multiple of these LIDAR sensors. To put it into context, most I2C devices have some open contacts on them to be soldered to change that specific device's address. These LIDAR sensors do not. The computer sees them all as the same addressed device. 

**Challenges:** After searching for a while we found the [solution](https://learn.adafruit.com/adafruit-tca9548a-1-to-8-i2c-multiplexer-breakout/overview)

![Adafruit Multiplexor](https://lh3.googleusercontent.com/gKi4F82c64VIzTMdUPSBchK0JifVvYcXCZDYRrkZKu2HJdEyvG_43-ixJnhnzBaNKqooZgQ9GivHG2mmE9KNf7ZBNYGMmikEPmD6v78CQIfT5TRT703zkyFA--JNJp50AJRo4qmhEtJ_LtYf3Q4PIzIRwqaettrii-OX4QT9K4lzJufzWImsHlGsABPXMvaO-96r6TDhof2M0L6gPVWiHxQ5e2ouC0wbclHMuld3SNm6beiRU5r4BliDHenp7GW5L2qedptk8aS7NGUzAii-CqagIVBeQYx-5x133HtTW_LCxYhJ9fpO0Exus6KB9ydvx2jhHNTJF6ATTEuLzYym7p72aC-PoARbvl_jMoeGXrnmRVRLQXJ3qOnxin5hQ7duxDZDTnVoUjU7efEMPd9c8uhHGPPinfrTNBm3GPjHTJnPZUcE9kXNf44Da7foSfj-zBg7bSwHRu-tlhxkEpG1KiAhcg7sfFjtCACcIhe1HFYKwDyNYQfMoSFjmdOt102eMUopZvGljn2_eaYiy-3zxkD9O8XZsC0Dlc8IVc8HzMeOn0HtPHvYrysKTwgaU_4Mq54tOOPjjBb7TaI_ICvMoASbKHLE-b7EpqpgBxDSYb18DvZQ7cntX0vcAq_i8j6JaQ3AJzjZt-uhtcEBvws3kUAHtcxk3kKPcxd8BAR5PA=w1288-h990-no)

   | The multiplexor itself has its own unique address. Essentially you just write to it which port you want to be connected to and it passes through the data and clock to that device only. 

**Moving Forward:** An order was put in at the end of the day for one of these. While waiting, I'll read through the avaliable adafruit library and prepare for the hardware arrival.

___

**Date:** 23 January 2017 Monday

**Objective:** 12a.Boat Game LIDAR Sensors

**Progress Today:** 

**Challenges:** 

**Moving Forward:**

___

**Date:** 

**Objective:** 12a.Boat Game LIDAR Sensors

**Progress Today:** 

**Challenges:** 

**Moving Forward:**

