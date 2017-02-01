## Console 11 Project Page: Static Magnetism
### Subprojects:
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

![Rotational Pneumatic Actuator](https://lh3.googleusercontent.com/PPz6Zcv4UFJUmy2MchgZ-pJox1gfgz2XyNEl0RGQiHupyGupCQqHkuXsPed3mMnVQcNHQSpvS22OB8NbL6o25axai3qybzyrmDhj3WwtQbfyDf4nh7X51WTLg0l5FEN9h3LRqYzLLeWnIYnrxFpu2MWoFWpzc801KVMI0WG9DgTbbXjOJcUMHJlPNeXFJ6AQJcre9HPyx9809hzwh2jlW8RBiiif-b6rEws8EcpAr6SkkJBNgVGTTdTkP4vnh3v6CtwSSLyU7RB8nl2RgZ1XzCq9_oYqupyQsgbZ8b6W2yfqRGlY4K5K37PCq4GHO11bsIulwuLfA6xSWgU2hlDu-X4_qtPewCY_ylGZ4wRgUPUkoOfFvG4qS0ApFidGu98ArvWrqxGLTzD1Nn0YRtJ8GHhCYwqSJKqIfRya7Dm29HJEzGRw5ACPLxxEsINzGfc36Ulsrbv_YffESiH8qDpclyvVYh9KRwudUS62Tla0flAHuI-DuP1ZbOwT_XnICu3ieHv0E_4HEz9_n5sn_hwvc87m243mUnXmVc9SyCk5zhESKq261tDxT9vEDyr_zfqVNcYRZJCy02vUfLD3PrVYTUthITi3Nxf7W7rnfkQCbufo9Ba9eROJSQAAKf7kpAr5OIUZ52s-BhP1_AWTP8uf4ZtlONV8xOytaEE0Fx5AKg=w1760-h990-no)

   | This method has a host of benefits: Its faster to cut the manufactuer the pieces, its sturdy, and tried and true. However, some notiable downsides were that it has multiple parts and is not super great for creating complex parts with varying features. As such, I decided to go with the 3D printed part which has increased manufacteuring time with the upshot of zero assembly time and complexity. 
 
![Ring Holder CAD](https://lh3.googleusercontent.com/_lPD_ciSYVSbcjpU2YU5N6TTFTU0On98Rxh3AVp3U0RyvwQA0j21M7j3tueGq7CsdbpAwLa3YkcwI1tP_14JYsYoz1GKw2AyD7PJgABuBkITMPQT10CYKH3WWBionOuS3pqOo4fyXsOKa7aEo022vPxNlHmiYPb2LjwVEfbLPXPkrcZednDPxvhFJaTLCnZgrFgCFJnVbaT_ven3vhlYqWy7uhwCBljkPTh4JoeZixzr9X2ZEwMzAXRfi7C4pcisWg0hDM_neJC3CmXgpnkNTKYrHbprksiyU7ZvVby08CFnW-tLd_-qhnG9NiEmLNvAS41_mZO4No-xyHuQQzzkDMTjCU6xOnhbXf7GQzDnC23ilj__pIw6PEOkhVJnYgs7UCn5f7pVsBNYMtcjC5PelOyLU89yxtE5nMVblMb6AT7SV-y8OSSbqS6Mge1oc6gGreCBvXbZh-aYLw_oYYz1nYbZOodFBPhpMKQtXgxRjlpwtmJQdl7mZhG1vdqPVlZJcG3h17cy0KIaMrCC2AJhixXAycmC6i9gY3Egn11nrlA7iDSsbKw69EQVpgUvaU5WMQM-V8iTHLNH12rRXPml82mQsxLoBFEOq6caZPkHWuyG0_KkUo4keVjwcNILyN0RxxHzykmuFpTDsVOf3h-TTl6HgiiZ66XLfRTwJalqFQ=w1159-h905-no) 
   | I CAD'ed up a model of the LED ring holder to fairly tight tolerance. The ring would be friction fit and/or super glued to the holder and the holder would be pressfit onto the permanent magnet. I referenced this [page](http://makezine.com/2015/07/22/tips-3d-printing-press-fit-parts/) and learned it would be easier to rely on plastics high pliability to get the pressfit I wanted. The described octagonal press fit sacrifies strength for a higher amount of tolerance, and is perfectly applicable in this implementation.

The Ring Holder would take about an hour to print. Thats fine in a normal sense, but I wanted to cut down on iteration time so I made a test ring.

![Test Ring CAD](https://lh3.googleusercontent.com/cKHnPZkBflcT5hMo6gtF2InERrYSU3je3IaQGP4nEqi4jgD5oHZQMQnNY15C8R0O8HGLDiNDrB8R3R1hjfr548fhV9YqZl8yDsdCJYlQa-L0LLGU2veYL0veDJRaIkAMD3wHiDSIoJrMloPPkcHtcezs0TIu_WiZumLFfVjactq0aESwZcbiAOgBnR0nIVgrpiUrplbbSUQOf0mAHQ9HUE-80h55Atnm3J1rZVkBv_AThJo3k4itKGdMIIZTVzU9-HrmaMg2szxw4cf70Bwy6X8NYn5HPMK-1tgdoWh9r7WeDqAom7g9I6XZgvSvdSC50-s-eGi0ikbGXro5Jkb7S4bjc-Fy2kvAS8q5xY-mLVqC_XBg2O6uTn7txaV7-7VrvHLz8RJ5-tlQOZVPTZdhwz2Rm7XaSF6z8k8vnJjgGmCKsgnJKo8NKAeypEu4BAsx1cmEiSmHe18KPanmEIiNWMjPSMFvVo4lwUWciOPROI4qTHMTMa12722nWMRGAMYe728G9z-brcs9S7GArSboxEfmnuxHV6fTYM20vxTZcCVIR9FcDX0fVQEKe8vv5qXTFjyrsjl0Lf1FzF4EHcZiiTPLbMX-N6gN1oNszPbWgUQ6EZwysa-56YimcFFLJmw-RKcV-9L9ccmY2I_Mvws7K4Rp76Rgk60eI_EDKl2l7w=w1125-h876-no)
   | Before printing the whole holder, I wanted to test the press fit. I made a simple ring of the same tolerance but using way less material which means less printing time. 
   
   | TEST



**Moving Forward:** 
