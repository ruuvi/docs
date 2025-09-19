---
noIndex: true
---

# Air 1st Stage Bootloader

The 1st stage bootloader is minimal, immutable firmware which initializes the board, provides a factory recovery option and starts the more sophisticated second stage bootloader.&#x20;

The bootloader is shipped with two cryptographic keys: Development and Production \[TODO link public keys]. Development key is shared to the world, and anyone can create their own firmware variants with development key. Production keys are internal to Ruuvi only for the security of users.&#x20;

By default, Ruuvi Air ships with only production key enabled. To enable the development key, factory reset must be executed. After factory reset, development keys remain enabled until production key is used for the first time. Development keys can be re-enabled with a factory reset.&#x20;

The flowchart of operation is below, legend:&#x20;

White: Ready, Green: Being tested, Blue: TODO. As of Air fw v0.1.5

<figure><img src="../.gitbook/assets/Air B0.png" alt="Air 1st stage bootloader. Press and hold button for at least 10 seconds while connecting power to run factory reset"><figcaption></figcaption></figure>

The first stage bootloader executes quickly, the button has to be pressed at powerup or reboot for the button to be registered. To run a factory reset, press the button for at least 10 seconds until bottom leds start alternating green-led blink sequence.&#x20;

To enter firmware loader for uploading firmware, release the button before 10 seconds have passed.&#x20;

Source code is available at [https://github.com/ruuvi/ruuvi.air.b0](https://github.com/ruuvi/ruuvi.air.b0)

