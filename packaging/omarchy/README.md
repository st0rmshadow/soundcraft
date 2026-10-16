# SoundCraft on Omarchy

Omarchy is PipeWire-first. This fork builds SoundCraft with cpal’s native **PipeWire** host
(plus ALSA), so Setup › Playback Engine can select PipeWire devices and buffer sizes directly.

## Build

```bash
cd ~/Personal/soundcraft   # or wherever you cloned st0rmshadow/soundcraft
git fetch origin && git checkout cursor/pipewire-audio-f910
git pull

# Headers (Arch / Omarchy):
sudo pacman -S --needed base-devel alsa-lib pipewire pipewire-alsa pipewire-pulse pkgconf

cargo build --release -p soundcraft
```

Optional JACK host (PipeWire’s JACK compatibility):

```bash
sudo pacman -S --needed pipewire-jack jack2   # or your distro’s pipewire-jack
cargo build --release -p soundcraft --features jack
```

## Run / smoke test

```bash
./target/release/soundcraft --demo --control 0
```

1. Open **Setup › Playback Engine**.
2. Audio system should list **PipeWire** (often the default) and **ALSA**.
3. Pick your speakers / interface, set buffer (e.g. 256), **Apply**.
4. Space to play the demo — you should hear audio through PipeWire.
5. Arm a track, record a take, confirm input meters move.

Agent / script check (with the app’s control port printed at start):

```bash
# List systems and the open device:
soundcraft-cli app --port PORT ui.audio_device '{"list":true}'
# Prefer PipeWire + a buffer size:
soundcraft-cli app --port PORT ui.audio_device '{"system":"PipeWire","buffer_size":256}'
```

## Remotes

| Remote   | URL |
|----------|-----|
| `origin` | `https://github.com/st0rmshadow/soundcraft` (this fork) |
| `upstream` | `https://github.com/storytold/soundcraft` |

Work on feature branches; open PRs upstream when a slice is clean.
