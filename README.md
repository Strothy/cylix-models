# Cylix models

Model files that the Cylix app downloads the first time a feature needs them. Nothing here is run on its own.

## AllTracker (release `alltracker-v1`)

The point cloud tracker in Cylix's Track panel. [AllTracker](https://github.com/aharley/alltracker) is by Adam W. Harley and is under the MIT licence ([LICENSE](LICENSE)). These files are its published weights, exported to ONNX:

| File | What | SHA-256 |
|---|---|---|
| `enc_ac16.onnx` + `.data` | the frame encoder (fp16 autocast export; weights stored in fp32) | `2c0d4d08…` / `0687bd40…` |
| `win_384x640_ac16.onnx` + `.data` | the 16-frame window refiner, landscape | `acfb35a4…` / `6ae4dfda…` |
| `win_640x384_ac16.onnx` + `.data` | the same, portrait | `7159ba17…` / `3df28b90…` |

The only change from a plain export: in the window graphs, `allowzero` is set to 0 on the Reshape nodes that never see a zero dimension, so DirectML accepts them. The results are the same.

Cylix checks each file's full SHA-256 after download.

## Parakeet (release `parakeet-v3`)

The speech recognition for Cylix's voice commands (English, German and 23 more languages). [parakeet-tdt-0.6b-v3](https://huggingface.co/nvidia/parakeet-tdt-0.6b-v3) is by NVIDIA and is under **CC BY 4.0**, not the MIT licence above: see the release's [LICENSE.md](https://github.com/Strothy/cylix-models/releases/download/parakeet-v3/LICENSE.md). These files are the int8 ONNX export by the [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) project (k2-fsa), redistributed unchanged. NVIDIA does not endorse Cylix.

| File | What | SHA-256 |
|---|---|---|
| `encoder.int8.onnx` | the audio encoder | `acfc2b44…` |
| `decoder.int8.onnx` | the prediction network | `179e50c4…` |
| `joiner.int8.onnx` | the joint network (tokens + durations) | `3164c13f…` |
| `tokens.txt` | the token list | `d5854467…` |

Full hashes and sizes are in the release notes.

## Kokoro British voice (release `kokoro-gb-v1`)

The British voice for Cylix's voice assistant. Everything here is under the **Apache License 2.0** ([LICENSE.md](https://github.com/Strothy/cylix-models/releases/download/kokoro-gb-v1/LICENSE.md) lists each file's origin and changes; [the licence text](https://github.com/Strothy/cylix-models/releases/download/kokoro-gb-v1/LICENSE-Apache-2.0.txt)). No GPL: no espeak-ng.

| File | What | From |
|---|---|---|
| `model.onnx` | Kokoro-82M v1.0 | [hexgrad](https://huggingface.co/hexgrad/Kokoro-82M), ONNX export by sherpa-onnx |
| `voices.bin` | the voice styles | hexgrad, packed by sherpa-onnx |
| `tokens.txt` | phoneme ids | same |
| `lexicon-gb-en.txt` | British pronunciation dictionary | [misaki](https://github.com/hexgrad/misaki) by hexgrad |
| `g2p-en-gb.onnx` | fallback for unknown words | [PeterReid](https://huggingface.co/PeterReid/graphemes_to_phonemes_en_gb), exported to ONNX for Cylix |

Full hashes and sizes are in the release notes. The authors do not endorse Cylix.
