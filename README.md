# [Hardware] Wave16
The Wave16 is a completely discrete hardware music synthisizer that is based on wavetable synthesis. It is constructed of TTL logic parts and contains ***no*** microprocessors or microcontrollers in its design. It's wavetable is 16 values long with each value having a resolution of 4 bits, effectivley forming a 16x16 grid. It also has implemented in hardware a decay envelope generator, a low-pass filter, and volume control. Sound waves can be viewed and edited on device, including the ability to archive waves in an EEPROM for later retrival and use. The shown device has been hand-soldered over 3 perfboards, and the case was made by hand using plexi-glass. 

![IMG_1488](https://user-images.githubusercontent.com/17792367/158073387-f1072235-8e9e-47f7-b21a-57a2c42677f6.jpg)

![IMG_1490](https://user-images.githubusercontent.com/17792367/158073390-4e4e4117-dcda-4943-b614-5bb9885a690a.jpg)


### Design
The Wave16's design can be broken up into 2 independent parts, the playback half (shown in orange and yellow) and the recording half (shown in blue and green). For this reason the design section will also be split to talk about both parts independently.

![Wave16 (1)](https://user-images.githubusercontent.com/17792367/149609945-75072161-6467-40a4-8e32-25f453558211.png)

#### Playback
Playback is relatively straightfoward. The loaded wavedata is stored in a 32byte RAM chip, whos adress is hooked up to a counter. The counter is fed by either an internal 555 clock or from an external source (for computer control). The output of the RAM chip goes to a 4 bit r2r DAC to create the analouge audio signal. This signal is fed to a decay envelope generator. When the generator is disabled, the audio signal is fed to the collector of a transistor, the base of which is connected to either the play switch or the external trigger. When triggered, the audio goes though the transistor unattenuated. When the generator is enabled on the other hand, a capacitor is put across the base of the transistor aswell, keeping the collector emmiter path open for a short while after the note is released. The legnth of the decay can be controlled by a variable resistor that is parralel to the capacitor. The transistor output is then fed to a lowpass filter and to a final volume adjustment potentiometer and is then finally output to a 3.5mm audio jack.

#### Recording
The wave recording process starts with the 16 wave input buttons. The signals from these are first converted into binary using a 16-4 diode array encoder. After this, the binary signals are sent to two diffrent circuits, a multi-input OR gate and the RAM's data input. The OR gate effectivley produces a positive pulse when any input button is pressed, which is then sent to the input processing stage, which is made up of a series of Schmitt Triggers. These first debounce the signal, and then manipulate it to produce the two signals needed for the RAM chip to write data (the binary data mentioned before) and for the binary counter to increment correctly. An edit button is placed inbetween the input processing and the RAM chips write enable to facilitate entering and exiting this edit mode. The permanent storage and retrival of created waves fro mthe EEPROM and facilitated internally by the RAM chip and are triggered using two push buttons.

### Development
This project originally began in the Summer of 2021 when i bought a bag of old recycled IC chips from Jameco Electronics. In the bag was a strange 64byte RAM chip with a built in EEPROM. I had originally dismissed the chip as useless, owing to its small capacity, but upon further reflection, I had a thought. The small capacity would of been just enough to store a few low resolution audio waves. With this in mind I decided to start work on a wavetable synthesizer. 

The playback portion of the circuit (pictured below) was a simple affair, being a scaled down version of the circuit I had first designed for my hardware PCM player. 

![IMG_1205](https://user-images.githubusercontent.com/17792367/158074476-b59fb777-0bce-4057-92c0-1eb58ce02277.jpg)

The circuitry to facilitate recording waves was much more time consuming process however, mostly due to the size of the diode decoding array and the amount of control signals needed.

<img width="927" alt="Screen Shot 2022-03-13 at 2 47 34 PM" src="https://user-images.githubusercontent.com/17792367/158074636-beda8920-3710-44c0-8c1e-c8a78212049c.png">

After the completion of the prototype came time for the soldering of the circuit onto a perfboard. This was also a time consuming process due to the number and intracacy of the connections. 

![IMG_1407](https://user-images.githubusercontent.com/17792367/158074738-d2af8e93-32a6-4f95-a4c0-ddd0c30f0800.jpg)

![IMG_1408](https://user-images.githubusercontent.com/17792367/158074745-6225736e-f799-4db9-bb58-e2bda9efeb51.jpg)

![IMG_1452-3](https://user-images.githubusercontent.com/17792367/158074751-25231708-5f6a-4d73-af94-f1376ccbd6ed.jpg)

With the electronics finished, all that was left to make an enclosure with some bolts and plexiglass, and the project was completed! This is at the time of writing, my favorite project I have done, being an order of magnitude more complex than any project I have done before. On top of this, it has directly helped spawn other projects such as my Python music sequencer and helped teach me much more about desining both digital and analog electronics.
