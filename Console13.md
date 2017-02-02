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

**Progress Today:** Today was spent testing the new mmultiplexor and creating the wiring harnesses to connect everything together. I pulled the code off of [Adafruit's Library](https://learn.adafruit.com/adafruit-tca9548a-1-to-8-i2c-multiplexer-breakout/wiring-and-test). 

After wiring the MUX up, I used [this code](http://playground.arduino.cc/Main/I2cScanner) to confirm the I2C device was detected on the bus.

I confirmed that the address was correct, *0X70*, and proceeded to connect one LIDAR sensor to the first port of the MUX. 

```cpp

#include <Wire.h>
#include <Adafruit_VL6180X.h> // REMEMBER TO DOWNLOAD THIS LIBRARY
extern "C" {
#include "utility/twi.h"  // from Wire library, so we can do bus scanning
}

#define Multiplex 0x70
#define IRSensor 0x29

Adafruit_VL6180X sensor = Adafruit_VL6180X();

////////////////////////// SELECT BETWEEN 0-3 //////////////////////////

const uint8_t port = 0; 

void TCASelect(uint8_t i) {
  Wire.beginTransmission(Multiplex);
  Wire.write(1 << i);
  Wire.endTransmission();

  Serial.print("Selecting Port: ");
  Serial.println(i);
}

void setup() {

  while (!Serial);
  delay(100);
  Wire.begin();

  TCASelect(port);
  digitalWrite(LED_PIN, HIGH);

  Serial.begin(115200);
  Serial.println("Starting Setup!");

  while (!sensor.begin()) {
    TCASelect(port);
    sensor.begin();
  }

  Serial.print("Sensor ");
  Serial.print(port);
  Serial.println(" found!");

  delay(2000);
}

void loop() {
  TCASelect(port);
  float lux = sensor.readLux(VL6180X_ALS_GAIN_5);
  Serial.print("Lux: "); Serial.println(lux);

  uint8_t range = sensor.readRange();
  uint8_t status = sensor.readRangeStatus();

  if (status == VL6180X_ERROR_NONE) {
    Serial.print("Range: "); Serial.println(range);
    digitalWrite(LED_PIN, HIGH);
  }
```

   | Connecting the MUX and LIDAR code was a bit trickier than anticipated. The function that switcheds ports on the MUX itself is called TCASelect. Once that was working, the device behaved normally.

**Challenges:** In the earlier hours I was plagued with reliability issues. The serial prints weren't working 90% of the time and I couldn't figure the problem out. I finally realized that the issue was with the setup of the serial and wire communications. 

```cpp
  while (!Serial);
  delay(100);
  Wire.begin();
```

   | I didn't think the problem was code side because the individual LIDAR and MUX code worked perfectly and I essentially copied them both together to make this sketch. This block ensures that both connections start properly.

**Moving Forward:** Tomorrow I'll work on getting multiple sensors wired and communicating properly over the MUX. 

___

**Date:** 24 January 2017 Tuesday

**Objective:** 12a.Boat Game LIDAR Sensors

**Progress Today:** Everything works! The system, with all sensors accounted for, is ready to be installed.

**Challenges:** I finished the rest of the ccables and wired all four sensors up. 

```cpp
void loop() {
  for (int i = 0; i < 4; i++) {

    TCASelect(i);
    uint8_t range = sensor.readRange();
    uint8_t status = sensor.readRangeStatus();

    if (status == VL6180X_ERROR_NONE) {
      Serial.print("Range: "); Serial.println(range);
    }
```

   | The code remained largely unchanged with the main addition being a for loop to iterate through the sensors.
   
I was curious to see if I had to declare seperate objects for each sensor or not. It was what I was used to, but from the microcontroller's point of view, there only ever exists one LIDAR sensor at the "same" address. After I confirmed it was working with four object declarations, I cut it down to a single LIDAR object. Code works fine; good to know.

Also finished up the soldering. Everything is ready to be mounted.

![Multiplex Board Breakout](https://lh3.googleusercontent.com/N4O-smY-kBe-XRoFcSlqJmnoJ9mCLqK97SX7ztYTTdxdJDHPvkxLUjFkIcaBiNdbJvHDDm2OoGZbHlqWZMLVIvlGwafJdm-2cGNJMYsJ-UB2zknXZe-TvrvcO3YksBRiMt_cSJ9D6wH39y6pnORRWdVUI3_dBI569vPRcgG3QqYG2GOh-ruvURuPJU3v6ZUQpSCmvYDmJHUrnUN76k_Y5LKTPpFOnyuE-6PyxMiswP_6wAj9B-yV5zawH3FGxVe04H4Zj-z9GmBOiKFnrWixWPRXQBDso2kA-lo2iuI_bKSlgTAUIAwRZCfg_wIUvAjrvDfWAZY-Maf7Q-7QNVcBdEYgNG3Au0A5alaOZ7D32w41gG_M2ns67tuydSygK0OqBTJASjUH-J5NaD-CxfJFKfe4sTJbnaJd5-H4LgWAZO2omV68C0m-pF2dDmTqh5oMEF6ug1MhKBsROTQU3_UGxYjxQ_NGur660W7Z2dw5a-KqlJYCq1zzb3YO_eZiZTPjEROD1OcaG6Z4mthnhrz9avPJgAr-luy8nP-XQZqr5PyzPJXS_DnV1rZMTqj1BmmpuaAWn2uLt7EWBNlhmEl87ygd_uRd4PhIVRB8cOlKMF-WtEf-=w546-h970-no)

   | Not the cleanest work I've done but we were on a time crunch. I made the wires with connectors so everything in the system can be taken apart and replaced without alteration to the other necessary components.

**Moving Forward:** Tomorrow I'll get everything installed. Templates will need to be made in order for the sensors to be mounted properly, and the position of the sensors is still to be determined.

___

**Date:** 25 January 2017 Wednesday

**Objective:** 12a.Boat Game LIDAR Sensors

**Progress Today:** Busy day today. Only finished the templates and finalized the positions for the sensors. 

For the templates, I snagged the origianl boat part off the DPEA vault and coppied the bottom curve. From there I just made a simple hole template with clearance holes to support the two mounting holes and the one big 8mm hole for the sensor. 

![LIDAR Template](https://lh3.googleusercontent.com/xfD5ksjuIbmfz_GG44tVFT2kcqBXaM6SXmEJhQfvlrkqkj_YFrBVCc1psHtEZmQjEjmy0t-V-P4JwBf8Qoi94vjMoW9syCaEDiBhHc5I5hyzJK9FRhYBzhcc5IIEPJxJM1jStOFE1lfthunMiEkqg1jQ0k9_N0e0wuq1tK6nIC8kSOipQuCLUF0ybzp7tELiXPQGOIicod43saeKdCJQsQEtjIm42tcrkVPig95MOgE64mX_ErbVUR4_Nrv2AL4KJLXpcnNhi0yIZjZrugckLxVX5dNLlYnq09Gf3xjmmvMjB4dxpPfEUkAfzA6Dg7KnfVQNZFGJ-m9ixBTiXeHfRW91Hy4UpJGuwqrq3FyTp4lJjFhx2ARV6qEodJ_6BtqtPOSishnh9p2x4WB1kAXbaWGckyGy48G3dpt7Qg3dUoam4v5m0HFt7umjsA5XPUfSnLHQ0UDGSr3wR1wuF8Y5DI4AoAOx1qljtO0WNmWT4mhTyflgY9FiILtn8Kw4md9Q_T48xUENnXjybPtlRWDo1G94uQuO-nUnHyulR9DEDuSArCbvLrspVZoZuMLcjFURlq4M0gY28YmBXxQbZqG-A91yzzeE5PVrD_kg7rOQQeeDw7Sv-YBCv60bDSlwVuKc8tevusjtxWJx2kp_OAG7rIe5YcXs9syThdU9f_MzYw=w919-h718-no)

   | I had to do a bit of guess work with the sensor clearance hole. The data sheet didn't have an explicit "Center" of the sensor Iso I did some empiracle testing before settling on this design
   
The hole positions were decided based on the boat home locations and where we thought the ball was guarenteed to pass by every time it transitioned from boat to boat.

**Moving Forward:** Tomorrow we'll drill the holes, mount up the sensors, and confirm the system works as intended.

___

**Date:** 26 January 2017 Thursday

**Objective:** 12a.Boat Game LIDAR Sensors

**Progress Today:** Everything checks out. I have 100% confidence in the system. The wiring and board mounting needs to be cleaned up a bit but the electronics and wiring are in full working order. Holes were drilled using the templates, sensors were mounted, and I confirmed that each sensor was reading through it's clearance hole.

![Boat Sensor Holes Front Install](https://lh3.googleusercontent.com/DMsmGsaPRXhLC_WZKXW5EV1qPXhyFqMC_SKo_arEo41XZfSiR-S5nSq_kSEr2_tCdSBVkz2JRU4ol-k4TDYjSMlGeeND_Q2YI0_atuk5EogWHYWB0lDi3Wsl-1YtX4tcxuq60yiMIBKIAgHimPuyVbn7OTJXkTVUyAcWKywdK9BhWyG2MEV_8oLr8onUw1Lm9kFO7g68IH1ApW-vQ5oXun6e_oUKOvTSmZNT8dzAE5M6bSrTSdUFi3xBFpjEk5g-AerIa6hOROW2sAAzpiHwnfwuhq3sa6N-CwQX4qPkrA8PlpCZ9-TY7X2fljs65ASHo3jq9K8QXFtE9POx0gdU_DpBEdZplbNA4X3IDwLWIxXDQFspPwR9qNd0-CIiohZJKaMAo-xs5wGsZhlsuQo_tVG08cGfrZo0I3YcVysxIjRqwRq8W-nskOxw9zXv-e-DYl0eLSofaXCflFL5owuAGOihtv1N0rmEE5D3esona4OVxbsXXZhP_7AWr-FvoHwUUMWqaYq0PpH8q6pkqwg6wRHgeGU2ccIadZryLz7YcyHr0aMXL3hHNc5XeUYw78X8DhoSnAkUuINHNDlMXNR2jKlxYNTCSo5Lmi2jZ2cR8QMHnpFn-0gZ7QbYqcRyU8dfYHGM2ZI-qu71ZR7SSsQGquqGiWDLjJgUXt3Dt9RIYA=w1760-h990-no)

   | Finished and installed sensors
   
![Boat Sensor Rear Install](https://lh3.googleusercontent.com/4sbG7Q8K3a6P6POin2xxEjxRN9KleYmQg1Eh-wze_6JqtrAZugL5LWr3w0fpTk3tv_S8mX25NNoQJmYM5UpsmWEOA-WhTDvVPHCYxWJTfEqRvN_q9XqHfqfbyx-x4wWV3TKJzDGiL6hrgOKC3K6CFjLvhBMvH5jlBHvE7tG8hM79O8sBZxXVmlOg3Hqz54-7_1x3JLeckD1BSydNTKT5MCRi3TNovTd1_EzpaaWHn9MUyngWmr2OE_O8szxLuYFqt9VRpxI60lvc92hbCRR2o_O9O4TqTchXtnXjmUZmiVX6AcgIginuPmlhD_52sJYlgidhxUywIvpSzT4Oq3R73LyIJbdohwJRzRsgjPPt5BKE9JpMTNzjB4Kin03fyjWY5JUaOd8kiXeFMFLGw0O6HmxfrXaTkJnYIPFHKj4b840FjnmNKZDNQtcjwcRafiJc7qHEWon1kg_IbQjVfOPztOXTUPN0tdXua1-4BBov1DIy7uq35aCsjlBwTxzoXgrjzg8U--LEN4rDJtNFW8hYpYmrkgi_G8tFYostZGIStQnLpAtY0X0uAwMnBacSJsVjVZkA2LLwL934myT5m4lLZwryZxwty8-1HlLVXSvJh0tgx6rwZHNHHDibLwHAjY5YjjA6AXUkc5kdiGISfK31TVIo1q2YZ14Xlz8lRHK_aw=w920-h517-no)

   | They were mounted using some nuts and 2-56 bolts. Wire routing is temorarily being handled by a lot of blue tape.
   
**Moving Forward:** We'll clean up the wiring and mounting but for the most part the system is ready to be handed off to the students.

### Boat Game LIDAR Sensors - **DONE**
___

**Date:** 

**Objective:** 

**Progress Today:** 

**Challenges:** 

**Moving Forward:**

