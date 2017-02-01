## Console 12 Project Page: Waves In All Dimensions 

### Subprojects:
   * [Kuntz Tube Volume Attenuation]() **DONE**

Check out the main page [here](https://TerrenceTran.github.io)

___

**Date:** 13 January 2017 Friday

**Objective:** 12a.Kuntz Tube Volume Attenuation

**Progress Today:** The Kuntz Tube is a subsystem that consists of:

1. Arduino nano function generator shield
2. 200W audio amplifier
3. Kuntz tube 

When concieved, the 200W amplifier was thought to have the ability to modulate its volume via digital control *IE: I2C, SPI, etc* However, it turns out that neither the function generator nor the amplifier have the ability to do so. Currently, the volume can only be changed via a potentiometer on the amplifier. The goal is to create an intermediate system between the two that will add this functionality.

**Challenges:** There are a couple of ways to do this. Today was spent brainstroming the different methods and their pros and cons. After much consideration it was decided that the faster and easier means of implementation will take succession over the more complicated systems. The latter method has the primary benefit of providing a truer sound, while the crude method will distort the signal somewhat. This is less of a concern for this particular system because of its working nature. It requires resonate frequencies rather than complex signals such as music or conversation. As such, the minor distortion will be slight, uniform, and will not affect its primary mode of operation while being cheaper, and simpler than the alternatives. Win-win.

**Moving Forward:** The easiet implementation would be a digitally controlled potentiometer with all the fixings. I must admit it is a somewhat daunting task due to my inexperience with communication buses, and hopefully I can source parts that only require a simple digital or analog line. It is what I and the students will be most familiar with

___

**Date:** 16 January 2017 Monday

**Objective:** 12a.Kuntz Tube Volume Attenuation

**Progress Today:** Drew up the plans and BOM'ed the parts for the build. Sent the PO out at the end of the day. Also bought parts for the more complex build incase this falls through. Time is much more valuable than saving some money on redundancy. 

![Original Circuit Design](https://lh3.googleusercontent.com/yrGs3dPKhOau1yISFIUUBmCXUfzhuavTw5f2iEmavd3ihlRGEJyl-YrpEEz5sKLThQpcNr9mVTurKZojAszPZ6tRuNORf60pU7PPInVRmx_fTFwAktFcomW_4-ttfxqJyV-1ffhIhkclypfx9wH_AI_4uwnHhaM2xnDwr0FkzeLh_DOhzTygpo2hcO4YrdZqDpiSNiFwPYMp0X1rU8tcMNlb4zl1urHG-qjfMB2DmCTDro5R2zFSxjB_E0WBxgmvotcV-Z4k_56FWgVX80wBOTnoh9jiBKPaq-ZxYwYSZcnp6cfHf9MjNrR71gOBtL5czLm8qxQv0pnln-XD88ZwWtc-XnYNqEvDWePi8uCeVUzTKpXRYseblnFazFhyGZW4fmhabGsdVI_rzsUq_xpWqt113cFHKmGapcXuEyxhoiSCtk-K-MZ1qmg8MWGn95GY7_7iqXGggxOgL1-RjKksiKMcJ390rFdZpfCdzvtLOLX2mmcW3f17MpuLZcd3pYNduRGn1gu_yqRvuOUmUKDJ9hlHiWF0tIcER1z-JoiPL918XLImMvdZmhWzyp-3aBIPzURJ8t4R-RlfKl9y0DRDzGJBsEy1WKpS4XYF2zPzu7AvSlAQ_wSKTvylO13xjwMdYnH4_wXLXn4_6zKGciK1QPOEqygzXz2IOtc9DhdUcQ=w100-h150-no)

   | Simple sound attenuation with a treble cap for proper frequency response

**Challenges:** 

**Moving Forward:** I haven't had a chance to fiddle with much serial communication. The plan is to dig through the archives and get a feel for I2C and SPI until the parts arrive.

___

**Date:** 19 January 2017 Thursday

**Objective:** 12a.Kuntz Tube Volume Attenuation

**Progress Today:** Learned the basics of I2C communication and simple implementation. Tried my hand by programming simple functions onto an Adafruit PWM board we had. Worked out pretty well, with no major complications.

```cpp
void setup() {
  Wire.begin();                    // join i2c bus (address optional for master)
  }

void loop() {
  Wire.beginTransmission(adress);  // transmit to device at specirfied address
  Wire.write(value);               // sends value byte to that adress
  Wire.endTransmission();          // stop transmitting
  }
```

**Challenges:** The implementation called for me to learn about the Arduino **WIRE** library. All you need to do is find the address of the device and begin transmission to the correct address. 

**Moving Forward:** I'll keep fiddling with what I can get my hand on in preparation for when the parts arrive. We'll see what happens.

___

**Date:** 19 January 2017 Thursday

**Objective:** 12a.Kuntz Tube Volume Attenuation

**Progress Today:** The parts came in today. I had to a bit of reading on how exactly to communicate with the device but the principle was the same. I found sourced some code that controlled a similar digital pot and modified it to suit the new device.

```cpp
// I2C Digital Potentiometer
// by Nicholas Zambetti <http://www.zambetti.com>
// and Shawn Bonkowski <http://people.interaction-ivrea.it/s.bonkowski/>
// Variable pot tester for console 12

#include <Wire.h>

// I2C Address of device
#define DEFAULT_ADDRESS  0x28  // A0,A1 & A2 are connected to GND

// Command definitions
#define WRPOT0 0xA9
#define WRPOT1 0xAA
#define WRBOTH 0xAF

// Common WIPER values
#define WIPER_MAX  0x00 // 0
#define WIPER_MID  0x20 // 32
#define WIPER_MIN  0x3F // 63
#define WIPER_MUTE 0x40 // 64

void setup() {
  Wire.begin(); // join i2c bus (address optional for master)
}

// this loop runs through values 0-64 to sweep the pot from high to low (low pin and sweeper pin)
void loop() {
  for (uint8_t i = 0; i<32; i++) {
  Wire.beginTransmission(DEFAULT_ADDRESS); // transmit to device 
  Wire.write((uint8_t)WRPOT0);   // A9 = write to pot 0 only, AF = both pots
  
/*Bits 0 through 5 of the register are used to set the position on the resistor array
  Bit 6 is used to set the wiper position to the mute position and bit 7 is a don’t care
  If the value of bit 6 is set equal to 1, regardless of all other bit values, 
  the wiper position of the respective potentiometer will be set to the mute position.*/

  // WRITE IN uint8_t !!! values from 0-64
  
  Wire.write((uint8_t)i);      // sends potentiometer value byte 
  
  Wire.endTransmission();     // stop transmitting

  delay(10*(32/(i+1)));
  }
}
```

   | To use this device, you need to connect to it first with ```Wire.begin()``` and ```Wire.beginTransmission```. Then there are two steps to writing the actual value desired. The first *Write*, ```Wire.write((uint8_t)WRPOT0)``` specifies which internal potentiometer to adjust. The scond *Write*, ```Wire.write((uint8_t)i)``` write the value as a byte, with acceptable values ranging from 0-64. 
   
The pot was tested fine, and the circuit was bread boarded and tested. Everything checks out. Everything was installed onto a permanent protoboard and soldered up. I put the option of both coupled and decoupled outputs, just incase the need arose. 

![Completed Function Generator Top View](https://lh3.googleusercontent.com/8Xz53yVcgIY5xsKu8-AWBn3NS9ZcI6R0Zi-4XMTI0_Wkswjd0j1LSvzmLonglK6sf7Ap1gwHBuQ1eSuZh3E_XGQLXrV_XfpQC6t_PNrC74asU6Qf2cnn3kUbNxRxCAY7Y4FwaaQIPA82Hy5FM69MFbDmSpAjbza4KvZb8aiE34dYt2EE4Ln2dOcNyWnjft_n1OJfxF-EBt_QJYFzY00TPzBnAnSPfPJwKlEzemUwXIIr2VO0q_mgM4eDRBEZ3k50BzCjcuuz9_YNDvy8kGRfdq_5NG3u8Wc9sBeklhEbK3AYbufEFAndr43IDz830WZ0Z1hGYQw2AHPlN-Y2yLnjYqNvDJzXoQ8b7fMroP-3Sn9Mz4KW0hjof7BmagQhWjAGlX-e01jX_tNfMddAWlJhYD21HGq4lNSwDrwRHw4TFw1SC4GPZwECI3lQdmq4SHtJGAAO6lS_mbQpPe1ObAocwjKN0ouHnlpjtrGTzi7bPQoKDwlSbjDr6JaFbGTHw_QH_Rn5EyGym_qxFHe-hM-uqJyEdj2e-8oIhBOu6cJfcYtN0dB0Nlq_A_QBmEaSpy_rzIYH2aiLT5E-UkrgoO_eGMszBJ-Nyg_bLHydDwjXkiy4AeAptMWz0vx12HagNL_6XC-Qe37d-wX-U0Xss4C5OEJe9yjhoobwnSvmWbxdqQ=w1760-h990-no)

   | Completed board. The three red boards are function generators and the 14 pin IC is the digital potentiometer. The pins to the far right connect this board to I2C and SPI interfaces on the arduinos.
   
![Completed Function Generator Profile View](https://lh3.googleusercontent.com/oFZ0lBuV0O5HzPxJBDTVWZ8QwsxgfsVMxESpHzW85s3U3Dfbo_JCU5fuR4jZNcHC1ZVdYNJ2KUWV2zSYBT5p8M28CgbU72Wlh9CnKtfImfEkGhkAFt2D1HoByy405ZnvqkO3_wlGkeGSgk5qZ28eTM420NCcUq75tr1T8A4gEpB56rrQVmnwkzp7a2HFloY9VD_Xlp4nnUR4aRBSPvKUZJlPXrCSdoc0Sri7nBG2obaopBokJgOJRpCOBZ27Eirv5rsi3KKs6RWzwk2AetIGaoQi7IzsThX-CdB0I4lBkfUlqYrQMK84CFDffJgodnobOelmoLZ8TQ2u5xkSni5KpyM1NfexeqSQYkdxqDVBpTQc3a3LKk3ultQYRLZKToht6rXJJqVBQ9spmED4SXP9rimnLKOuUL5JtfNSC7JLXPwsi7VwGPbe_ZBv9khyueqDJ_C05mFBGYTxokcRo1FcaRO1CXPMleVbO3ItSCcezxLChoAjQ0chZkEQoRks2lmy2IpGsSqzJXFs298siwJvmZOrWpU5AF0OIU41TUhFP-5Da5CDtWTQZumyVkbrwkMt0sJipI4RyKmr0yaOfkFjSnTHVqizrihhKnJG6ikVO_DHDA5kYOcuHntNdcMnUWsBXo73hdxd5Y1Q3oxPJCC_tb-wIKTZr_5aRuLfprJ5Fw=w1760-h990-no)

   | Compact and ready for mounting 

**Challenges:** The hardest part of this project was starting the communcation over the I2C serial port. After some trial and error, everything came together. 

**Moving Forward:** Tomorrow the system will be installed and tested with the Kundts tube. Everything apart from this sub system is working fine, and the code will take a little porting before ready. 

___

**Date:** 20 January 2017 Friday

**Objective:** 12a.Kuntz Tube Volume Attenuation

**Progress Today:** The modulation works but the range is of adjustment is very minimal. Although the pot has 64 discrete positions, the volume attenuates to something inaudible after the first 10 steps. 

**Challenges:** Using a phone app we cheecked to see how much the voume was changing between steps in terms of dB. We learned that each step dropped the sound roughly 2 dB. The drop was linear along the dB scale. We concluded that the volume taper is fine but the range of adjustments leaves a lot to be desired. To fix that, we added a coupled resistor.

![Circuit With Range Modification](https://lh3.googleusercontent.com/pVDUvdcoicgn5EI7RcbVmHaVETdKPVP77rsgjJHZjD4WSwH7qzZNSg9zElnISYw6MzC9DbCT3R_Css0l1GoTG2Hc9a_ydhKBkm65luK2ZEo9ctapK4TGsJBFCC1avXJ9JxBSu79s157bb1MjdX2_2td6WT37mWSwQeXWJ_4w0Sh3m8NS845xRDFL-WQrC4-0Tmi2ji5RbgkOE9djc7E7-YcapnelOOP2ewLU6mYQ3Yqx4m45khz8F2zcpSdBajKCS-_aSkKLsa8_HNmrQ3FUpQAJx8k616CPw5TV7iR0gwVQh5lEIW7Z0EB2vQYZJyNIEwq4nDM2IiGF2t5L2K1Emaf2u-E5--cJ90U4DYkKZ5Strx9cWehyfP77M9UzdtcGT5BAxMS6B33YGl-DxHr5YT3uk7KfKn4tm6FSqM4nspal-8SxWNWXrE2G2OZlMq6y5I2Y_JDu7kYVbHVlepnRnRCD7lmbxjNZQEfleLHfN9QcP2hXTz-Ws1gj_EwFoFAujvxhcb15EP-E7jrSqM8HmTKiGS7b2NGOmubU-V5zXOdpSiWNwSGDKf74hpIpm6teBwrFEpqi6h1XLKaFPft2Bot-yFl4rZSvF-ZLKj23QdEbsdsJI4Y4nhW33CGRL345dmidzAwS5PyIYGdT5b5L4oXb7S7cryUC0kXpol1p7w=w125-h200-no)

   | Adding the resistor extended our range by about 4x which is plenty of attenuation steps. Originally, the digital pot had a range from 0 - 47kOhms so we added a 22kOhm resistor to couple the wiper and high terminals. It was a fast and simple solution.
   
**ADD VIDEO HYPERLINK**

 ### Kuntz Tube Volume Attenuation - **DONE**

___

**Date:** 

**Objective:** 12a.Kuntz Tube Volume Attenuation

**Progress Today:** 

**Challenges:** 

**Moving Forward:**
