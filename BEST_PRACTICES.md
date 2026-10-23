# Best Practices

## Every device must have these (or we fail)

1. **All passwords encrypted.** Use `secret` instead of `password`, and turn on `service password-encryption`.
2. **SSH only, no Telnet.** Set `transport input ssh` on the VTY lines.
3. **HTTP server off.** Run `no ip http server` on every switch.

## Working on the .pkt file

- Only one person edits the .pkt at a time. It can't be merged, so two people editing it means someone's work gets overwritten.
- Pull before you start, and push as soon as you're done.
- Tell the team in Discord when you start and when you push.

## Saving configs

- When you finish a device, save its `show running-config` output as a text file named after the device (example: `MLS0.txt`) in `configs/`.