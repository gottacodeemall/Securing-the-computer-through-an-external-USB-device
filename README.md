# Securing-the-computer-through-an-external-USB-device

Making the following changes at the kernel level will ensure that the boot process will complete only when a usb device of a certain key is inserted into the i/o slot.

The correct device must be inserted in less than 100 seconds or within 5 attempts.

## Compiling and Installing the kernel

1. make config localmodconfig
2. Replace the hardcoded USB serial number with that of your device.
   - This is found in drivers/usb/core/hub.c.
   - **Note:** Some USB devices, like HID devices, won't have a serial number.
3. To compile your kernel using 4 physical cores.
   - `sudo make -j 4 && sudo make -j 4 modules_install`
4. To install the compiled kernel.
   - `sudo make install`
5. Update grub and propagate the changes to grub loader.
   - `sudo update-grub`

## Use Case

- This will enable the user to add an additional layer of authentication.
- If the user had physically locked down their computer, password protecting the BIOS changing computer’s boot sequence to disallow booting from removable media, then this addition to the GNU Linux kernel would indeed add some measure of additional security.If the user had not implemented the aforementioned security measures, this system could easily be overcome by installing a new linux partition and using the computer.
