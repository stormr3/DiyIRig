# DiyRig 

> Creating a DIY IRig (Audio Interface) so that my friend stops using his electric guitar like an acoustic.

## Why I'm building this?
My friend had the money to buy an electric guitar but not to buy a Pedal, so naturally he went for the cheaper option, an IRig. But being the genius he is, he ordered it to the wrong place and is now just using his guitar like it's an Acoustic. And I cant hear Wonderwall once more.

## The Beginnings
Now being an ECE guy I thought what even is an IRig, cant we just connect the guitar to a laptop directly since it gives a signal we could pass through the aux and then use a digital software for effects and play it through a speaker? I tried that with my friend the moment the idea struck me and tbh we both didnt think it'd be that simple, but surprisingly we got sound. It was shit for sure, but wayyy better than anything we expected. But I cant be calling myself an ECE guy by just connecting two wires to an aux can I.

## The Hurdle: Tone Suck
First I found out the reason for the shit sound. Its a phenomenon called Tone Suck. It happens because our guitar has a high impedance, and we connect it to a laptop mic jack that has a relatively low impedance (it’s a 2.2k ohm load meant for cheap PC headsets). When they connect, it basically acts as a massive low-pass filter and murders all the high-end treble of the guitar.

## The ECE Fix
Now this sounded similar to an project I had done previously, but exactly the opposite. In that project, I was using the laptop aux jack to drive an 8-ohm speaker, so the laptop jack was the one with the higher impedance. That circuit was a bit more complex because we needed to actually amplify the voltage, but I remembered testing the speaker with a simple buffer (emitter follower) circuit and getting decent results.
So in this case, it's way simpler. We don't need a massive power amplifier to drive a speaker; we just want to protect the fragile guitar signal. We pass the raw signal into the laptop, and the software handles everything else.

## The Scrap Bin Parts List:
I built this using literal leftovers from the previous project. It's super cheap:

* **1x 2N2222 Transistor:** The main workhorse.
* **1x 9V Battery:** Powers the circuit (and lasts practically forever).
* **2x 1M ohm resistors:** These divide the 9V in half so the audio wave has room to swing without clipping.
* **1x 10k ohm resistor:** Keeps the idle battery drain ridiculously low.
* **Capacitors (0.1µF/10µF):** You need these at the input and output to block DC voltage so you don't fry your guitar or laptop. *(Pro tip: If you only have tiny 0.1µF caps, stack a few of them in parallel at the output, otherwise the circuit cuts out your bass frequencies!)*

## Does it work?
Idk. I ran an AC sweep in LTspice. Plugging straight into the laptop killed the high-end treble by -45dB. With the buffer in the middle, the EQ curve stays almost perfectly flat in the frequencies I want. I'll update as soon as I get it up and running 

## How to use it
Plug the guitar into the circuit input, run an aux cable from the output to your laptop's mic jack, and open up an amp sim like Amplitube or Guitar Rig.
