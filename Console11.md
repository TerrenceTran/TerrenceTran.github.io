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
   | Before printing the whole holder, I wanted to test the press fit. I made a simple ring of the same tolerance but using way less material which means less printing time. The test ring took about 6 minutes to print and also fit very well on the frist try.
   
Although I knew the real ring holder would have four times the surface area, I wanted a bit of a tighter fit. I shrunk down the octagonal part by about two thousanths and printed it out. And hour later it came out like this.

![Printed Ring Holder With Supports](https://lh3.googleusercontent.com/Uc5YvMwpv0b3pzqY3RL0kzMd2Jhhuyl7EAmcTwCBcUOGPIuthVMUEamIOqWGz21HCOIT931ZEK0cnyOqos_Xp5t_mzhQ5klxJjW0uLA8tr8A-_9_zy0WDeUGX-KoLZS1-CSeoxKYio0O3ZwjJRYy4SmPECBNHJ5FXZaSMC9usoVaMAdaMhTsgtJip2TCktBCpi9dVNWZ6VoNM1L1VlK2JEgkltHIbo43fAUtliJjHyRaL4r64J4CXF6allnwxE934zDSYhSy703slereqrUblFbZU-x0AljAi4FZDW2YGNoHYFL6NKLidoO5Uc4STnmN1L4beSOllRrXBOAh6mM8H85Tx0cwxjAE1ZJ6ISqkOsbdOOEYxCOLTOHKsZtXvhfLhNpEZ4JheV5iR_sMK2Goqlw7_AwOhcrp2eDnkVkhOw1HWSMn_xDXvKArAbvb5JgnKE7IwDi64e5QZdMSytLgbNhquFOg-HCasMH3tvk7P-5ci5r1NNG4-T1jBDLlGwtrOlxysLoYc5j7IyZAILldT3GbRt7U1eKQsl31ndULhZ3q_Q3TcrlLGNDaYu3o3Np8D2HFiOjERoAbFDQOj9UC4wBHat-qgew123UY1xneOkzEQq8Aj8GG9D49hXoTqsTFIyHwnGus_ZLMvur6YT5CwqX_iZh2sw8FLRD_URBrAg=w1760-h990-no)
   | Support material was needed because the part needed to be printed upside down to insure a better surface finish. 
   
![Printed Ring Holder Without Supports](https://lh3.googleusercontent.com/YwI2jaPAg-4LvRYt4uLCuTrNKzxOS6FfXUK1ql2SWcYpB4FSqeZWVJqxLC6A8ify7ekshxN8M3MXyvXLZ_nTcizYpJXwLCzReudOym9lMURwYUAZZKuT4gznVEGKYkw7alVoqgC9Wo_zjt1WyhkvleeRHkQuov4yiqUH68P4PfeNB4O6i3FnYp2AR7MXJtwnmTSHrybN5D1XwUzCKbgcBQFMUAD_ZKz0lJcGO3mPl6vwvrWkPKkugfGfP9id966eWGtoy9dsxikd44epcFzmiFsJsaczfrO-mnMJ6voNdZbqUgzJLV4yQ12FtRttuiE6vy8sFFgLd0WBbr-JWOWRkrSV01pE9Sp9jd8TMX4R5azc4_Tb2s1lQ-o94OlinsfMLJwSX0GWzUVjSVrI-vmTaqGBdCvymiK-ho7Xqy7AvKNMOJ-FTqdDmW-WJ_ZO_gJUNhQpsnd1Oghv9rCkaIASX8xLRTj2rKcbski8jazfTyelD7WxwxbNP6E5fxqzYDBC5aRmbXhddeSpyPnV89RkweZtQN1SRqVH4A3c48cRSvuwTDoxq1lus9VSvmQiE3J3JQqS5DB-Hqoi6xoFIKb2xoL6kL-4iLbwGp5dhfKnRzi-b_nNBtU863AMBzS_o5qv3ZbUxJU9uX85zxLklnVmx3CUTK9LirNJKOgrmR04Lg=w1760-h990-no)
   | Supports came off easily enough.
  
**Moving Forward:** I'll stop here for today because the magnet is still installed on the game. Tomorrow, we'll test the final fit and finish. Here's to hoping.

___

**Date:** 1 January 2017 Wednesday

**Objective:** 11a. Vertical Maze LED Ring

**Progress Today:** This morning we tested the fit and finish of the holder. The results speak for themselves.

![Finished Ring Assembly Side View](https://lh3.googleusercontent.com/p1DRG1_IX8Sr4Q0EDcT_qZ4s5C38n8rDwfJreHyNO6xvfpyWuPrNGpY0OoR0FNLF7iYzGSl6MzvrrH2rn9XxQOvFuusUJ4e8CBsyn7hwBqwOcW1dyoc2kzndEpIjzcyooaYm2u1DDS2NDOsu6a9rHCihxUYERCj2FwFku7x-E_jp5YQ3eTNScuK59YqzxmfnD67X9NGxtYSZKS3E0quK57m4Zu0Q6InPE-uoi1FQJ1cZXUhhX5F93Vb63xS3YP1g1ipXBV3YcaxgNZOZ6zJL6NJd7RKKwkytn-Xp0P6BNHzFvgkuT5hIhRkXI-9UpczSo_Qgbss-kIHBJg5wDn3s70RQCBvf8drTef47qzrHERSB8uClEDnog5o5FNH30gOdGfB1LY7fLOckg0TV0GsLan4lf2PASKSx8JoUY-l1S27m9SlFZuNMNuglbaKP6GIr5K3rXHjfxNqeCYYcrgWP8usQlEmTTdrEx6wCgzPMOgTeWBOcUsAqZbpGods8XT4iTx7szTMT1Z1X0osJWP-l4seK2H3Lbss25myHb7XLrVYiXHOOkoX60j3O2rZpAOOG3ZKaeKw0UHDdeUlDoDaFGrRLnzEWv0d7hmx6pn2z4zfT77Hfr0Npal94p_TlJhuHl0Gb5lecXN2YEqme8QmbdD9vzrqOQtAnfxEWtNH9rA=w1760-h990-no)
   | The press fit is super snug. The plan was to use super glue to keep everything in place but that wasn't required at all.
   
![Finished Ring Assembly Top View](https://lh3.googleusercontent.com/ZVfZfStp6pMpxiEEwuKusGQ9bPBWuyMUdRFSCc6__C53HrPME77EXaag_jvVe8QVyJAumjynpBy-11ehwAjsiucVf-i04O7d-7NMQMDAGzyroIKid3romBmnm57lsI_6eR8F0ZcylbFNXVKwK2LmjauBiQAo0hQO4aajPdM7z23vxIpyeURaiMiWUTahBk0hEtDhLoTusC2pS0pQBhYDaNwzwzgKK-9lA4Ny1a_WNLov8sg7NC54tNF9aH4yszackR5cH6gEvWJbGH-LW0haRJpUP5Bi1-5S2-N9-ArxEWf5ZFhbU9nBlkJeCfyXPjnzyYM0XTs2T0xXgloAvArKUdKj9XnPiFsyy7xmkpY5Ox1FZiEBbL4zXOVT-tK6bn2RVjYk2dN3-OF6Tl-zZeD9Wh2vXh6Nq8dPIDUg_tVXjh38SRfxXotHB0DlBE7A7L09FEsSYycBP5y04oIT5odMBfP3H1V1J_kl6E0KLXxYUk1QODydmOAnkr7qJ-bJHJKMjSjnE4HAnISJCN73_ZWyJomRhugOveiKydx52RI58T4Ra59JY0bIFWa1F2YR0E3PY6UI_xq59K2W6Xo6cx6raeg5c-W_31GaVIz7bNfO4aqwbJe6=w1760-h990-no)
   | Top view showing the ocatagonal pressfit. The LED ring fit snuggly with the #D printed circumference aswell. 
   
![Ring assembly Installed](https://lh3.googleusercontent.com/Mpc1dYPlY5pNhOLG2jurm_jg0vnm25nDfjeFBI1W-_v3Yagv0oES8xg-r6GaL6iShlRxSNAooZvKqrUxuo5eLWE7Vej3Efi775gPaW48bk2bpCTE97fKESKjWU2IZxSve7l3MGnvsUSB2bq9Wesn6LMzTGr5eCo8Cicls0Z1qcqeLnISqelzDQk0mNqah8MDLoPHdU0vp3qTXbRrfulrDEwGX_vsW4TBo0eJ7l4DbtvBkRHaOEBOEG8qkZ3QO_T_dvKg8C2_prQ6dcs3Bnwb7iPUp4Sqi7LrPnDiVs-zRnPZB0p2y_s2WLQXkjma3xVFzoAbBB-8gjHh9ndkHuFz1p12zh3HbP_a_rl6X6m6CHmfBXxw2gyEBzpNUhxnowa3tG8oPfzSZAfsylIePkmPPQzP7FcRmOeu4HDPRE_RQRfoWfH27quBJnCQT7u2wQ4shz3Cy-D56wQF4v4WmHrYjOmgxsPqyVqf_RixE34dF_JqRIhAa0k_t-sNLaknGsvds2V-CjxecTiqcOcj7rrfQKbSaY30bhbboyppHXTpQlygCLBsqNxNx0P9f14ZFv1jGpvobV13XGSH1_OCCDT5dSetbiBjupOc_jpgDdtvcFzNsbHolnUj=w1760-h990-no)
   | And here's everything installed onto the maze mecahnism. 
   
After installation, the ring and maze were tetsted and working just fine. All that's left is for the sstudents to take the wheel and program everything. 

## DONE

___

**Date:** 

**Objective:** 

**Progress Today:** 

**Challenges:** 

**Moving Forward:** 
