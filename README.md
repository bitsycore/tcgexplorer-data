# TCG Explorer data

Files the [TCG Explorer](https://play.google.com/store/apps/details?id=com.bitsycore.tcgexplorer) app
downloads, published as GitHub releases. No code lives here: this repository exists so the files stay
downloadable without an account, whatever happens to the app's own repository.

| Release | What | Used for |
| --- | --- | --- |
| [`scan-models-1`](../../releases/tag/scan-models-1) | Card-scanning models: ONNX for Android, compiled CoreML for iOS | Downloaded once, when the user asks, before the first scan |
| [`riftbound-data`](../../releases/tag/riftbound-data) | Riftbound: a set list and one file per set, in the app's own model | Riftbound's catalogue; replaced in place when the data changes |
| [`wuwa-data`](../../releases/tag/wuwa-data) | Wuthering Waves: Battle: a set list and one file per set and language (ja, ko, zh-cn, unofficial en) | Wuthering Waves' catalogue; replaced in place when the data changes |

## Card data format

- `setlist-v1.json`: every set (`CardSet`), and for each its files by language with name, size,
  SHA-256 and card count. The app reads it first, at most once a day.
- `set-<code>-<language>-v1.json.gz`: one set's cards (`CardPrinting`) in one language, gzipped. The
  app downloads it when the set is opened, checks it against the set list's SHA-256, and downloads it
  again only when that hash changes.
- The `v1` is the format: a newer format is published beside it, so older builds keep working.
  `riftbound-v1.json.gz` is the earlier single-file Riftbound format, kept for older builds and no
  longer updated.

The app checks each model file against a SHA-256 it carries before using it. Asset URLs are stable:
`https://github.com/bitsycore/tcgexplorer-data/releases/download/<tag>/<file>`.

## Licences and sources

- `card_corners_640`: card corner detector, trained from scratch on synthetic data. MIT.
- `card_embedder`: torchvision MobileNetV3-Large with ImageNet weights, cut at its 1280-d layer.
  BSD-3-Clause (torchvision); the weights were trained on ImageNet.
- Riftbound card data: from [Riftcodex](https://riftcodex.com/), an unofficial fan project not
  affiliated with Riot Games. Card names, text and artwork belong to Riot Games; images are not stored
  here and stay on Riot's CDN.
- Wuthering Waves: Battle card data: Japanese, Korean and Simplified Chinese from UCP's official card
  list ([wwcg.ucp-jp.com](https://wwcg.ucp-jp.com/jp/card)); where a printing has no record in a
  language, its card number's official text from another printing, marked as such. English is TCG
  Explorer's unofficial translation, marked as such. Card names, text and artwork belong to Kuro Games
  and UCP; images are not stored here and stay on UCP's CDN. Not affiliated with UCP or Kuro Games.

TCG Explorer isn't endorsed by Riot Games and doesn't reflect the views or opinions of Riot Games or
anyone officially involved in producing or managing Riot Games properties.
