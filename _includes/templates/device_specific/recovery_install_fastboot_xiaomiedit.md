{% if site.data.devices[page.device].custom_twrp_codename %}
{% assign twrp_codename = site.data.devices[page.device].custom_twrp_codename %}
{% else %}
{% assign twrp_codename = site.data.devices[page.device].codename %}
{% endif %}

## Installing a custom recovery using `fastboot`

{% if site.data.devices[page.device].custom_twrp_link %}
1. Download a custom recovery - you can download [TWRP]({{ site.data.devices[page.device].custom_twrp_link }}).
{% else %}
1. Download a custom recovery - you can download [TWRP](https://dl.twrp.me/{{ twrp_codename }}). Simply download the latest recovery file, named something like `twrp-x.x.x-x-{{ twrp_codename }}.img`.
{% endif %}
2. Connect your device to your PC via USB.
3. On the computer, open a command prompt (on Windows) or terminal (on Linux or macOS) window, and type:
```
adb reboot bootloader
```
    {% if site.data.devices[page.device].download_boot %}
    You can also boot into fastboot mode via a key combination:

    * {{ site.data.devices[page.device].download_boot }}
    {% endif %}
4. Once the device is in fastboot mode, verify your PC finds it by typing:
```
fastboot devices
```
    {% include tip.html content="If you see `no permissions fastboot` while on Linux or macOS, try running `fastboot` as root." %}
5. Flash recovery onto your device:
```
Depending on what MIUI firmware version you currently have on your device you may need to live boot into your recovery rom first and then flash it.
Currently all versions above MIUI V9.5.17.0 and Beta V8.7.5 have "Anti-Rollback". 
fastboot flash recovery twrp-x.x.x-x-{{ twrp_codename }}.img
```
    {% include tip.html content="If your device is currently" %}
	{% include tip.html content="The file may not be named identically to what stands in this command, so adjust accordingly." %}

6. Now reboot into recovery to verify the installation:
    * {{ site.data.devices[page.device].recovery_boot }}
