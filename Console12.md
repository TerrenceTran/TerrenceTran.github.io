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

**Progress Today:** 

**Challenges:** 

**Moving Forward:** 
