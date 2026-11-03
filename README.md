# TCG Explorer data

Files the [TCG Explorer](https://play.google.com/store/apps/details?id=com.bitsycore.tcgexplorer) app
downloads, published as GitHub releases. No code lives here: this repository exists so the files stay
downloadable without an account, whatever happens to the app's own repository.

| Release | What | Used for |
| --- | --- | --- |
| [`scan-models-1`](../../releases/tag/scan-models-1) | Card-scanning models: ONNX for Android, compiled CoreML for iOS | Downloaded once, when the user asks, before the first scan |
| [`riftbound-data`](../../releases/tag/riftbound-data) | `riftbound-v1.json.gz`: every Riftbound set and card in the app's own model | Riftbound's catalogue; replaced in place when the data changes |

The app checks each model file against a SHA-256 it carries before using it. Asset URLs are stable:
`https://github.com/bitsycore/tcgexplorer-data/releases/download/<tag>/<file>`.

## Licences and sources

- `card_corners_640`: card corner detector, trained from scratch on synthetic data. MIT.
- `card_embedder`: torchvision MobileNetV3-Large with ImageNet weights, cut at its 1280-d layer.
  BSD-3-Clause (torchvision); the weights were trained on ImageNet.
- Riftbound card data: from [Riftcodex](https://riftcodex.com/), an unofficial fan project not
  affiliated with Riot Games. Card names, text and artwork belong to Riot Games; images are not stored
  here and stay on Riot's CDN.

TCG Explorer isn't endorsed by Riot Games and doesn't reflect the views or opinions of Riot Games or
anyone officially involved in producing or managing Riot Games properties.
