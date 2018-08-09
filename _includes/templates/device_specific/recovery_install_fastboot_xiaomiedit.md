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
    * If your device is using MIUI V9.5.17.0 or MIUI Beta V8.7.5 and below you may use this to flash recovery.
```
fastboot flash recovery twrp-x.x.x-x-{{ twrp_codename }}.img
```
      Otherwise to circumvent the new anti-rollback feature included in firmwares above MIUI V9.5.17.0 or MIUI Beta V8.7.5 you must first use this
```
fastboot boot twrp-x.x.x-x-{{ twrp_codename }}.img
```
      Now once you have booted into recovery copy your recovery image to your phone then select "Install", now select "Install image" and now navigate to the directory where you saved your recovery image, open it and select your Recovery partion and swipe to flash. 
    {% include tip.html content="The file may not be named identically to what stands in this command, so adjust accordingly." %}
    {% include tip.html content="If your unsure whether or not your device has the new anti-rollback feature you can run `fastboot getvar anti`, if it comes back with 3 your fine but it comes back 4 your device has it installed." %}
    {% include warning.html content="With this new feature rolling back to an older firmware of which you currently have installed will **BRICK** your device. Do **NOT** try to rollback to an earlier firmware" %}
6. Now reboot into recovery to verify the installation:
    * {{ site.data.devices[page.device].recovery_boot }}
