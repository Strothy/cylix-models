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

## Model pack P (release `parakeet-v3`)

Third-party model files for a Cylix feature. [parakeet-tdt-0.6b-v3](https://huggingface.co/nvidia/parakeet-tdt-0.6b-v3) is by NVIDIA and is under **CC BY 4.0**, not the MIT licence above: see the release's [LICENSE.md](https://github.com/Strothy/cylix-models/releases/download/parakeet-v3/LICENSE.md). These files are the int8 ONNX export by the [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) project (k2-fsa), redistributed unchanged. NVIDIA does not endorse Cylix. Files, sizes and full hashes: the release notes.

## Model pack K (release `kokoro-gb-v1`)

Third-party model files for a Cylix feature, all under the **Apache License 2.0**: [Kokoro-82M](https://huggingface.co/hexgrad/Kokoro-82M) and [misaki](https://github.com/hexgrad/misaki) by hexgrad, a fallback model by [PeterReid](https://huggingface.co/PeterReid/graphemes_to_phonemes_en_gb), ONNX exports by sherpa-onnx. [LICENSE.md](https://github.com/Strothy/cylix-models/releases/download/kokoro-gb-v1/LICENSE.md) lists each file's origin and changes; [the licence text](https://github.com/Strothy/cylix-models/releases/download/kokoro-gb-v1/LICENSE-Apache-2.0.txt). Files, sizes and full hashes: the release notes. The authors do not endorse Cylix.
