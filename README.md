# [Hardware] Wave16
The Wave16 is a completely discrete hardware music synthisizer that is based on wavetable synthesis. It is constructed of TTL logic parts and contains ***no*** microprocessors or microcontrollers in its design. It's wavetable is 16 values long with each value having a resolution of 4 bits, effectivley forming a 16x16 grid. It also has implemented in hardware a decay envelope generator, a low-pass filter, and volume control. Sound waves can be viewed and edited on device, including the ability to archive waves in an EEPROM for later retrival and use. The shown device has been hand-soldered over 3 perfboards, and the case was made by hand using plexi-glass. 


### Design
The Wave16's design can be broken up into 2 independent parts, the playback half and the recording half. For this reason the design section will also be split to talk about both parts independently.
#### Playback
Playback is relitivly straightfoward. The loaded wavedata is stored in a 32byte RAM chip, whos adress is hooked up to a counter.    
