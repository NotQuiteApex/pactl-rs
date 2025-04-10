# Rust PulseAudio Control

[![docs](https://docs.rs/pactl/badge.svg)](https://docs.rs/pactl/) [![crates.io](https://img.shields.io/crates/v/pactl)](https://crates.io/crates/pactl)

`pactl` is a high level wrapper around the PulseAudio bindings supplied by `libpulse-binding` to make application development easier. It provides simple access to sinks, inputs, sources and outputs allowing one to write audio control programs with ease. This library is only capable of modifying PulseAudio data (e.g., changing volume, routing applications, and muting).

This is a fork of [`manuelVo/pulsectl-rs`](https://github.com/manuelVo/pulsectl-rs) with `sink-source-name-mixup` branch merge and some minor updates, which is then a fork of [`JojiiOfficial/pulsectl-rust-fork`](https://github.com/JojiiOfficial/pulsectl) which is then a fork of [`krruzic/pulsectl-rust`](https://github.com/krruzic/pulsectl).

### Example

List all currently connected playback devices.

```rust
use pactl::controllers::SinkController;
use pactl::controllers::DeviceControl;

// create handler that calls functions on playback devices and apps
let mut handler = SinkController::create().unwrap();

let devices = handler
    .list_devices()
    .expect("Could not get list of playback devices.");

println!("Playback Devices: ");
for dev in devices.clone() {
    println!(
        "[{}] {}, Volume: {}",
        dev.index,
        dev.description.as_ref().unwrap(),
        dev.volume.print()
    );
}
```

For more detailed examples, check the `examples` directory.
