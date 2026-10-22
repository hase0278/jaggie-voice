# jaggie-voice

Voice files for the **jaggie-video** Claude skill when it runs inside claude.ai's code-execution sandbox,
which can reach github.com but not Hugging Face.

| File | What |
|---|---|
| `kokoro-v1.0.onnx.part00` … `part06` | [Kokoro-82M](https://huggingface.co/hexgrad/Kokoro-82M) v1.0 (`kokoro-v1_0.pth`) exported to ONNX **with the duration output** (needed for word timestamps), split into 45 MB parts. Reassemble in order; the SHA-256 is in `manifest.json` |
| `am_michael.npy` | JAGGIE's voice: Kokoro's `am_michael` style vectors (510×1×256 float32) |
| `en_core_web_sm-3.8.0-py3-none-any.whl` | spaCy English model used by the misaki G2P (same version as the PyTorch pipeline) |
| `manifest.json` | Part list, sizes and checksums, read by the skill's `cloud_setup.py` |

Reassemble by hand:
```sh
cat kokoro-v1.0.onnx.part0* > kokoro-v1.0.onnx && sha256sum kokoro-v1.0.onnx   # compare with manifest.json
```

## Licences

* **Kokoro-82M** model weights and voices: Apache License 2.0, © hexgrad. https://huggingface.co/hexgrad/Kokoro-82M
  The ONNX file is a format conversion of those weights (no retraining); export script from
  [kokoro-onnx](https://github.com/thewh1teagle/kokoro-onnx) (MIT).
* **en_core_web_sm** 3.8.0: MIT License, © Explosion AI. https://github.com/explosion/spacy-models
