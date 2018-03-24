# Overview

Computers can help you roast coffee at home! This project is a collection of various things I'm experimenting with, mostly based around a [FreshRoast SR 700](http://www.burmancoffee.com/equipment/freshroast_SR_700.html), [Openroast](https://github.com/Roastero/Openroast), and a [Raspberry Pi 3](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/).

In the short-term, I just want to try programming various sensors and control systems, to see what helps in the home coffee roasting process (and what doesn't). There are many possible sensors that can feed input to a Raspberry Pi (cameras, microphones, thermometers, etc). Combining those sensors with the ability control the SR 700's heating element and fan speed could lead to many interesting possibilities.

Long-term, it would be great to have a multi-sensor computer system controlling the entire roast. 

# Sensors

Initial work will focus on various sensors, to quantify and detect physical values related to coffee roasting. A major requirement is that all sensors must be driven by the Raspberry Pi, since the long-term goal is to use these as inputs to control algorithms.

## Temperature

This is the classic value to measure in coffee roasting. The SR 700 provides temperature measurements, but its thermistor is below the roasting chamber, so it ends up measuring the temperature of the hot air before it hits the beans. It's common to also measure the temperature in the beans.

Currently I'm using a [PT100 platinum RTD sensor](https://www.adafruit.com/product/3290) with a [MAX31865](https://www.adafruit.com/product/3328) connected to the Raspberry Pi. With the PT100 placed right in the [FreshRoast's sweet spot](http://www.roastgeek.com/wordpress/2010/05/19/roast-temperature-probe-sweet-spot-in-fresh-roast/) it seems to be very accurate. See the [max31865](max31865) subproject.

## Sound

As the coffee beans heat up during the roast, they make "cracking" sounds. First crack and second crack are important points in time to note during the roast. I plan to use a [small microphone](https://www.adafruit.com/product/3421) placed near the roasting chamber as input to come kind of audio-processing program to detect the cracks.

## Vision

A [Raspberry Pi camera](https://www.adafruit.com/product/3099) could be used to monitor both the color of the beans during the roast, as they progress from green to tan to brown, and the downward velocity of the beans as the fan moves them through the roasting chamber.

An [RGB color sensor](https://www.adafruit.com/product/1334) might also be interesting for more precise color measurements of both whole and ground beans. This is the sensor used in the [Tonino](https://my-tonino.com/).

# Controls

For now, I'm just relying on [Openroast](https://github.com/Roastero/Openroast) to control the roaster. Its time-step-based programs are "good enough" for now. Their [freshroastsr700](https://github.com/Roastero/freshroastsr700) Python library would be a good way to start writing control programs, although eventually I'd like to build from the ground-up in Scala.
