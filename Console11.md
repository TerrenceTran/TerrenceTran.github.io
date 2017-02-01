## Console 11 Project Page: Static Magnetism
###Subprojects:
   * [Vertical Maze LED Ring]()

check out the main page [here](https://TerrenceTran.github.io)

**Date:** 30 January 2017 Monday

**Objective:** 11a. Vertical Maze LED Ring

**Progress Today:** To add to the playability of Console 11, an LED ring was to be added so that the user could see where the magnets were behind the scenes. The LED ring is an (Adafruit NeoPixel Ring)[https://www.adafruit.com/product/1643], chosen because of its easy of programing and connection. 

**Challenges:** I tested the ring after reading the guides and library examples. Works like a champ. 

```cpp
void setup() {
  ring.begin();
  ring.show(); // show makes them show their current setting. by default this is off
}

void loop() {
  // For a set of NeoPixels the first NeoPixel is 0, second is 1, all the way up to the count of pixels minus one.

  for (int i = 0; i < 3 * NUMPIXELS; i++) {

    // pixels.Color takes RGB values, from 0,0,0 up to 255,255,255
    if (i < NUMPIXELS)
      ring.setPixelColor(i, ring.Color(0, 255, 0)); // Moderately bright green color.

    else if (i < 2 * NUMPIXELS)
      ring.setPixelColor(i - NUMPIXELS, ring.Color(0, 0, 255)); // Moderately bright green color.

    else
      ring.setPixelColor(i - 2 * NUMPIXELS, ring.Color(255, 0, 0)); // Moderately bright green color.

    ring.show(); // This sends the updated pixel color to the hardware.

    delay(75); // Delay for a period of time (in milliseconds).

  }

}
```
   | The code is straight forward and follows the library examples closely with a few tweaks. Installation was fairly easy due to the ring's inbuilt resistors. Tomorrow I'm going to hand off the ring and this code to a student and give him free reign on what he thinks should be done. 

**Moving Forward:** The plan is to 3D print a pressfit mount to mate the LED rings and the permanent magnets. I was concerned that the heat created by these LED's migh cause deformation in the PLA plastic mount. I'll run the LEDs for a few hours and check thermals occasionally to be sure. 

___

**Date:** 31 January 2017 Tuesday

**Objective:** 11a. Vertical Maze LED Ring

**Progress Today:** LED thermals were checked and deemed safe under and circumstance. I had the ring running on full power for 2 hours and it heated up somewhat but maintained a comfortable contact temperature. The 3D printed mount is being fabricated as I speak.

**Challenges:** I was concerned about pressfitting 3D printed parts. I have made some prints in the past and the tolerance was off by as much as 50 thousanths so I was skeptical of the result. There was another option avaliable, which was to laser cut the needed peieces out of acrlic and screwing the layers together, eg:

!(Piston Rotational Actuator)[]

   | This method has a host of benefits: Its faster to cut the manufactuer the pieces, its sturdy, and tried and true. However, some notiable downsides were that it has multiple parts and is not super great for creating complex parts with varying features. As such, I decided to go with the 3D printed part which has increased manufacteuring time with the upshot of zero assembly time and complexity. 
   
I CAD'ed up a model of the LED ring holder to fairly tight tolerance. The ring would be friction fit and/or super glued to the holder and the holder would be pressfit onto the permanent magnet. I referenced this [page](http://makezine.com/2015/07/22/tips-3d-printing-press-fit-parts/) and learned it would be easier to rely on plastics high pliability to get the pressfit I wanted. The described octagonal press fit sacrifies strength for a higher amount of tolerance, and is perfectly applicable in this implementation.



**Moving Forward:** 
