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
