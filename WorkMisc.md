## DPEA Miscellaneous Project Page

### Subprojects:

   * [Infinity Mirror LED Driver]() **DONE**
   
Check out the main page [here](https://TerrenceTran.github.io)

___

**Date:** 2 Febuary Wednesday 2017

**Objective:** Infinity Mirror LED Driver

**Progress Today:** This was a one day project that got closed out the same evening. We ran out of drivers for RGB LED strips so I slapped one together. I used an IC that had controllable darlington pairs. All of our LED strips are common annode so I used a NPN chip to take advantage of that. The chip doesn't require external power and draws a small amount of current from the signal lines.

![RGB LED Driver Circuit Diagram](https://lh3.googleusercontent.com/kYD-y5Y-_TnZ53KxJ9WH6E_OIV-HfCWbvnloxK3-_rBj4Z3Vbx8tDPdYDIf3h82aIe6-iL6YgVyaop1W8n04nAlBzjRhyzNtA-N86u-ma4TgMP6oDAMOtfavfTDpu5I3R9fOhCZcQOr-GML06uojMXSIidEv3h0RdPUvXFPZXAShA1HCQXoKW52_Bx4AV366bk7C_FuDuDwLtEecY4q-UdDz17-q211BrjxB_7FOaYqgSe69BzOBPK1zyqUs3qgczK1YF1WnRhZl0vT91xr0gYZ16-yz4xOLNgid46wUP2Qc2kCbsXCS7_Z-mtm5bF1C_XSlTm5iSpQG00YLjEQezi0VlShfdXgknwRJkwqCTWekFcqTIlSYdeeIRd_UvxxL3zzD6P-KwIMlG351out1fRBq6hSg4EE9pH3qu09aZZndvvAfxfYExenURjYnnPemI7mDRlCwkHEiIzIBpkWR7or-A0phkwRqtsEvuTfgrpK-dSbBDRCYNUE-FcLjOPLTfuwKlnZ-X5Y3MwKPjJt_ipoKR8a8rWMWEwiDfrKRNigOz-JbRYlMaR444yBwbqWilyBfPkJJ4R4xAD0T6PYLT82uTpFBgkXfhFzt4F7JN7xaYrMtMR-Z207bfVg_TnQg6QG4Lwnu1sSAF9kAU4fO6kPKx0wIzIyqFSgdXmbQkA=w1760-h990-no)

    | Left lines are input signals to control the LED strips. They can be written to via an Arduino's `<analogWrite()>` function and the brightness can be varied from 0-255.
   
![RGB LED Driver](https://lh3.googleusercontent.com/QsYyGcJoioCL0C4QEPUXli_uuKoEhNuKH3GsPnAFY8c5aFnYlmqFlnz6UsM3-2Td-2lLwF7AI_nZbrnFgD6S6U_ZaDM6uOpTqjpwu8l8Rh44miarQt-JfE01VODyj5ow3rTECTgZTuAxxvfxbrRWfL1Qe-5osSbRdnf8-QEAPRkVddP-bUYxpJRxMzKvAjduvo31e_XRAseu_oGu4MP0DkBUE7I8_kZaZkquvzfuHZoF8ubZHreLYVeIxNK7aUpG11jritixiHZqX-y3kC0XEwvbPfe8owaRN0nwzTH3B4tHzk7j-3P3NTI-dbctw2FGBZDhPCUXaTvGh5ix_nRVmcY0kfHe4boUteZ0cUWVT9nQtqDx6wrOThYF25P3tqcP2GZCm_ScKo7n0VZgOlm0M0gNaxJSgWqPS4MA5OPlVkMyDiYlNa-i-yvBbQjAZ_BtBD_S5vXgkd0vEJpG7CfEDtv3adxv1h1vmDFEAdk6_GUrHT6OqmyUsZPxZPdhle4ysxVM_tXl8PLRNWPzRPY0NAW9Sp1SkHfJSmYoguj4kYwFb2lqjGW-CM8d3-d_n1coNysauJ_K8BGYRFYR3EOA7y1Oqwf0miOHvBZMSX4d0L-AE-GpVZxTLsTglENISToc-s4061LhfyobvPUDhOCKrzY3-sqY0NjOxDY4gkuDfQ=w1760-h990-no)

    | Completed and soldered board.
   
![Finished Infinity Mirror](https://lh3.googleusercontent.com/i1uaqcbd7warjX6CNcITizjVemcElIFEe6gjVULg6SGWgVWHo76VgnKYQcHNIW7AGblsFSydYoe2JJkkFwgFkG5AZEjwhHPLDtt9qVG88HOzL1XobxdyMqLmtkv_xoq_l6HgH0u2DMFFIU4M04m7Uihu1TjKIOAYQH_VrUsvNAnQPbY5fiDaV3k94uC4DqYeTbVGrJGkzgG35zXy8RLz_xFFZIHxyT4UkIO6mNBB0LQWqPCN1AAccX62dGIw8zuEGFnP65r6DPXRu3ndUDEaVubjG2HUSDXII-YkuHKhpTLLgyjXPal3QXrvIvjZRvK-B4dIdLozvXgVKOjYR1cCUuqr6o4cUzFxpx6GJR-mkxQHGfM07XD09pjTC88noN8ip_XN40as-WMHGteTfARTQBeJ_8Qx-dPfQDcl2x8zdupEdTC8cd4gyzotAy54tqJWOGascMwecr56xP9eDvLHzDJor2q_FgORpsL0KRZOHCiwWcS7TGcRXul5-4MxShkKnWbvEurPqXSWJp6oCQnzseQdaN9JttVtScH31XN0vEzRBaJd_U0FbJZDkvye1IqrYRbYZpER6wP70vYFpADcCMhWJcTKYg9w0N3cOsXA4fULzlPTeIvpP6uHMQf3NcKfLAEfSdKizyWHkkkK7wNtU5MLh2HbIloz0GwgauGQjw=w557-h990-no)

    | Finished project. Make sure the intensity attenuation worked and closed it out.

**Moving Forward:** The project was quick and dirty. It was nice to contribute to something so cool. The mirror will now fall into the hands of extremely capable students. I can't wait to see their progress.

### Infinity Mirror LED Driver - **DONE**

___

**Date:** 

**Objective:** 

**Progress Today:** 

**Challenges:** 

**Moving Forward:** 
