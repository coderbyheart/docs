# nRF Cloud AGPS Sample

The `nrf_cloud_agps` sample is the *easiest* way to get started with generating GPS coordinates with your nRF9160 Feather.

## Programming `nrf_cloud_apgs` **Sample**

As of this writing, this example works best using a fork of nRF Connect SDK. You can skip the compilation step and download the update binary [here](files/nrf_cloud_agps_nrf9160_feather.bin).

1. Change directories to `ncs/nrf`
1. Make sure that you're running the latest master. Running `git fetch` and then  `git checkout bb259bfad1fa3572563444edb512fc8a6f12a3f4`.
1. Run `west update` to fetch all dependencies
1. Then change directories to `nrf/samples/nrf9160/nrf_cloud_agps/`
1. Add this to `prj.conf`:
   ```
   # Cloud prefix for nRF9160 Feather
   CONFIG_NRF_CLOUD_CLIENT_ID_PREFIX="feather-"

   # Enable Zephyr application to be booted by MCUboot
   CONFIG_BOOTLOADER_MCUBOOT=y
   ```

Then compile as normal:

```
$ west build -b circuitdojo_feather_nrf9160ns
```

Then load using `newmgr`:

```
$ newtmgr -c serial image upload build/zephyr/app_update.bin
$ newtmgr -c serial reset
```

**Note:** fixes in this fork will be merged into the nRF Connect SDK main branch soon.

## Setting Up nRF Cloud

During factory test, your nRF9160 Feather is added to nRF Cloud for your immediate use! The only thing you'll need, other than your nRF9160 Feather, SIM and antenna is your getting started card:

![Cloud Code](/img/agps-sample/nrf-cloud-code.jpg)

Every nRF9160 Feather has a device ID generated based on the IMEI. Your full device ID will look something like:

`feather-<IMEI>` where `<IMEI>` is the IMEI tied to your specific device. You'll need this in a moment.

Here are the steps to get you the rest of the way.

1. First, program your device with the `nrf_cloud_agps` sample.
1. Then, power up and confirm that the device can connect to the cloud.
1. Create an nRF Cloud Account
   ![Add new device](img/agps-sample/add-new-device.png)
1. Once created, go to the top left and click the big **+** icon.
   ![Add LTE device](img/agps-sample/add-lte-device.png)
1. Then skip the iBasis setup since we're using Hologram.
   ![Skip iBasis](img/agps-sample/skip-ibasis-setup.png)
1. Enter the Device ID and the PIN provided on your card.
   ![Enter device ID and pin](img/agps-sample/enter-device-id-and-pin.png)
1. Once you press **Add Device**, nRF Cloud should notify you that your device has been added!
1. Navigate to **Devices** and click on the device you're working wtih!
   ![Devices](img/agps-sample/devices.png)

That's it!

Your device screen will adapt to the example code that you're using. For example, it should display a map when you begin to publish GPS data.

![nRF Cloud Screenshot with map](img/agps-sample/nrf-cloud-screenshot.png)

