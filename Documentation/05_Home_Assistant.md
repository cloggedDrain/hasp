# Home Assistant integration

Upon startup the default HMI display file contains empty buttons with no text.  You must send the device its configuration when it connects to your broker.

## MQTT

This project relies on [MQTT](https://home-assistant.io/docs/mqtt/) for device communication.  You will need to enable Home Assistant MQTT support by adding the following line to your `configuration.yaml`:

```yaml
# Example configuration.yaml entry
mqtt:
```

If you don't already have an MQTT broker configured, adding this one line will enable the built-in MQTT broker.

## Recorder

The [Home Assistant Recorder](https://www.home-assistant.io/components/recorder/) component is required to allow Home Assistant to save configuration and state of some HASP controls across reboots.  You will can enable Home Assistant Recorder by adding the following line to your `configuration.yaml`:

```yaml
# Example configuration.yaml entry
recorder:
```

## Packages

The configuration and automation files for the HASP are bundled as [Home Assistant Pacakges](https://www.home-assistant.io/docs/configuration/packages/).  Enable packages under the `homeassistant` section at the top of your `configuration.yaml` by adding the following line:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

Now, copy the entire [`packages` folder structure](../Home_Assistant/packages) to your `.homeassistant` folder and restart Home Assistant to pull in your changes.  You can do this on your Home Assistant installation with the following commands:

```bash
cd ~/.homeassistant
bash <(wget -qO- https://raw.githubusercontent.com/aderusha/HASwitchPlate/master/Home_Assistant/deployhasp.sh)
```

Once Home Assistant has restarted, launch the web UI and look for a new tab with your chosen device name.  Select that tab and look for the automation titled `hasp_<your_device_name>_00_FirstTimeSetup`.  Select that automation and click "TRIGGER" to apply the basic configuration to your new device.

![Home_Assistant_FirstTimeSetup](https://github.com/aderusha/HASwitchPlate/blob/master/Documentation/Images/Home_Assistant_FirstTimeSetup?raw=true)
