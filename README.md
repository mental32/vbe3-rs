# vbe3-rs
## A no_std crate to help with writing VBE3.0 drivers.

## Index

 - [Examples](#Examples)
 - [History](#History)

## [Examples](#Index)

### "Hello, World!" with VBE Controller Information

```rust
use vbe3::{VBEHandle, VBEInfoBlock, functions};

struct Stub;

impl VBEHandle for Stub {
    fn enter_real_mode(&mut self) -> vbe3::Result<()> { /* ... */ }
    fn exit_real_mode(&mut self) -> vbe3::Result<()> { /* ... */ }
}

fn kmain(/* ... */) {
    /* ... */
    let mut vbe_handler = Stub {};

    let vbe_info_block = vbe_handler.with_real_mode(|| {
        functions::return_vbe_controller_information()
    })?;

    kprintln!("{:?}", vbe_info_block);
    /* ... */
}
```

## [History](#Index)

### An introduction to VBE

The VESA BIOS Extension (VBE) standard was established to standardize a
modular, software interface to display and audio devices. The VBE interface
is intended to simplify and encourage the development of applications that
wish to use graphics, video and audio devices without specific knowledge of
the internal operation of the evolving target hardware.

The VBE standard defines a set of extensions to the VGA ROM BIOS services.
These functions can be accessed under DOS through interrupt 10h, or be
called directly by high performance 32-bit applications and operating
systems other than DOS.

These extensions also provide a hardware-independent mechanism to obtain
vendor information, and serve as an extensible foundation for OEMs and
VESA to facilitate rapid software support of emerging hardware technology
without sacrificing backwards compatibility.
