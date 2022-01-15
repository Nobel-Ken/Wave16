# [Hardware] Wave16
The Wave16 is a completely discrete hardware music synthisizer that is based on wavetable synthesis. It is constructed of TTL logic parts and contains ***no*** microprocessors or microcontrollers in its design. It's wavetable is 16 values long with each value having a resolution of 4 bits, effectivley forming a 16x16 grid. It also has implemented in hardware a decay envelope generator, a low-pass filter, and volume control. Sound waves can be viewed and edited on device, including the ability to archive waves in an EEPROM for later retrival and use. The shown device has been hand-soldered over 3 perfboards, and the case was made by hand using plexi-glass. 


### Design
The Wave16's design can be broken up into 2 independent parts, the playback half (shown in orange and yellow) and the recording half (shown in blue and green). For this reason the design section will also be split to talk about both parts independently.

![Wave16 (1)](https://user-images.githubusercontent.com/17792367/149609945-75072161-6467-40a4-8e32-25f453558211.png)

#### Playback
Playback is relitivly straightfoward. The loaded wavedata is stored in a 32byte RAM chip, whos adress is hooked up to a counter. The counter is fed by either an internal 555 clock or from an external source (for computer control). The output of the RAM chip goes to a 4 bit r2r DAC to create the analouge audio signal. This signal is fed to a decay envelope generator. When the generator is disabled, the audio signal is fed to the collector of a transistor, the base of which is connected to either the play switch or the external trigger. When triggered, the audio goes though the transistor unattenuated. When the generator is enabled on the other hand, a capacitor is put across the base of the transistor aswell, keeping the collector emmiter oath open for a short while after the note is released. The legnth of the decay can be controlled by a variable resistor that is parralel to the capacitor. The transistor output is then fed to a lowpass filter and to a final volume adjustment potentiometer and is then finally output to a 3.5mm audio jack.
