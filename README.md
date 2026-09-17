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

## The Hurdles
During the physical build, the biggest hurdle was getting a 10uF capacitor which I had to pest a guy continuously to get (thanks to him tho). 

<img width="1280" height="720" alt="BreadboardCircuit" src="https://github.com/user-attachments/assets/7424bef8-2943-4483-a62c-f1cd743f0d9a" />

Jokes aside, the first real hurdle after making the circuit and plugging the guitar in was the noise. There was a constant hum (check out the 1st demo with the circuit). I was disappointed as this was worse than directly plugging it in, but there was a weird familiarity with the sound—it was kinda similar to the hum we hear near transformers. Then I realized I was using an AC to DC power supply and it was injecting that noise into my circuit. Simply replacing it with a battery killed that issue so much so that there was literal silence when the guitar was not being played.
The next hurdle was the latency. It still sounded pretty bad due to the delay, which was also messing up the person playing. This was rather a simple fix because it was a software issue, so we used a different audio driver: ASIO4ALL. And with this, everything suddenly clicked. The project was complete. 
Well, it was still on a breadboard, but whoooo cares.

## Improvements to be made
- [ ] Transfer the circuit to a perfboard.
- [ ] Have Proper connectors for the 3.5mm and 6.35mm audio jacks.
- [ ] (Ambitious) Create a casing for the circuit to make it a user viable product.

## The Scrap Bin Parts List:
I built this using literal leftovers from the previous project. It's super cheap:

* **1x 2N2222 Transistor:** The main workhorse.
* **1x 9V Battery:** Powers the circuit (and lasts practically forever).
* **2x 1M ohm resistors:** These divide the 9V in half so the audio wave has room to swing without clipping.
* **1x 10k ohm resistor:** Keeps the idle battery drain ridiculously low.
* **Capacitors (0.1µF/10µF):** You need these at the input and output to block DC voltage so you don't fry your guitar or laptop. *(Pro tip: If you only have tiny 0.1µF caps, stack a few of them in parallel at the output, otherwise the circuit cuts out your bass frequencies!)*

## How to use it
Plug the guitar into the circuit input, run an aux cable from the output to your laptop's mic jack, and open up an amp sim like Amplitube or Guitar Rig.
