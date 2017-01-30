## Console 12 Project Page: Waves In All Dimensions 
###Subprojects:
   * [Kuntz Tube Volume Attenuation]()

check out the main page [here](https://TerrenceTran.github.io)

**Date:** 13 January 2017 Friday

**Objective:** 1.Kuntz Tube Volume Attenuation

**Progress Today:** The Kuntz Tube is a subsystem that consists of:

1. Arduino nano function generator shield
2. 200W audio amplifier
3. Kuntz tube 

When concieved, the 200W amplifier was thought to have the ability to modulate its volume via digital control *IE: I2C, SPI, etc* However, it turns out that neither the function generator nor the amplifier have the ability to do so. Currently, the volume can only be changed via a potentiometer on the amplifier. The goal is to create an intermediate system between the two that will add this functionality.

**Challenges:** There are a couple of ways to do this. Today was spent brainstroming the different methods and their pros and cons. After much consideration it was decided that the faster and easier means of implementation will take succession over the more complicated systems. The latter method has the primary benefit of providing a truer sound, while the crude method will distort the signal somewhat. This is less of a concern for this particular system because of its working nature. It requires resonate frequencies rather than complex signals such as music or conversation. As such, the minor distortion will be slight, uniform, and will not affect its primary mode of operation while being cheaper, and simpler than the alternatives. Win-win.

**Moving Forward:** The easiet implementation would be a digitally controlled potentiometer with all the fixings. I must admit it is a somewhat daunting task due to my inexperience with communication buses, and hopefully I can source parts that only require a simple digital or analog line. It is what I and the students will be most familiar with

___

**Date:** 16 January 2017 Monday

**Objective:** 1.Kuntz Tube Volume Attenuation

**Progress Today:** Drew up the plans and BOM'ed the parts for the build. Sent the PO out at the end of the day. Also bought parts for the more complex build incase this falls through. Time is much more valuable than saving some money on redundancy. 

![Original Circuit Design](https://lh3.googleusercontent.com/yrGs3dPKhOau1yISFIUUBmCXUfzhuavTw5f2iEmavd3ihlRGEJyl-YrpEEz5sKLThQpcNr9mVTurKZojAszPZ6tRuNORf60pU7PPInVRmx_fTFwAktFcomW_4-ttfxqJyV-1ffhIhkclypfx9wH_AI_4uwnHhaM2xnDwr0FkzeLh_DOhzTygpo2hcO4YrdZqDpiSNiFwPYMp0X1rU8tcMNlb4zl1urHG-qjfMB2DmCTDro5R2zFSxjB_E0WBxgmvotcV-Z4k_56FWgVX80wBOTnoh9jiBKPaq-ZxYwYSZcnp6cfHf9MjNrR71gOBtL5czLm8qxQv0pnln-XD88ZwWtc-XnYNqEvDWePi8uCeVUzTKpXRYseblnFazFhyGZW4fmhabGsdVI_rzsUq_xpWqt113cFHKmGapcXuEyxhoiSCtk-K-MZ1qmg8MWGn95GY7_7iqXGggxOgL1-RjKksiKMcJ390rFdZpfCdzvtLOLX2mmcW3f17MpuLZcd3pYNduRGn1gu_yqRvuOUmUKDJ9hlHiWF0tIcER1z-JoiPL918XLImMvdZmhWzyp-3aBIPzURJ8t4R-RlfKl9y0DRDzGJBsEy1WKpS4XYF2zPzu7AvSlAQ_wSKTvylO13xjwMdYnH4_wXLXn4_6zKGciK1QPOEqygzXz2IOtc9DhdUcQ=w100-h150-no)

   | Simple sound attenuation with a treble cap for proper frequency response

**Challenges:** 

**Moving Forward:** I haven't had a chance to fiddle with much serial communication. The plan is to dig through the archives and get a feel for I2C and SPI until the parts arrive.

___

**Date:** 19 January 2017 Thursday

**Objective:** 1.Kuntz Tube Volume Attenuation

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

**Challenges:** The implementation called for me to learn about the Arduino <WIRE> library. All you need to do is find the address of the device and begin transmission to the correct address. 

**Moving Forward:** I'll keep fiddling with what I can get my hand on in preparation for when the parts arrive. We'll see what happens.

___

**Date:** 19 January 2017 Thursday

**Objective:** 1.Kuntz Tube Volume Attenuation

**Progress Today:** 

**Challenges:** 

**Moving Forward:**
