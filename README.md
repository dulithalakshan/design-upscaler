# Design File Upscaler

**Live site:** https://dulithalakshan.github.io/design-upscaler/

Free, in-browser AI upscaler for the images inside **Photoshop (.psd)** and **Affinity (.af / .afphoto / .afdesign)** files. No server and no API keys. Files never leave the user's computer.

## Publish on GitHub Pages (free)

1. Create a new **public** repository on GitHub, e.g. `design-upscaler`.
2. Upload `index.html` (and this README) to the root of the repo. Use **Add file → Upload files**.
3. Go to **Settings → Pages**. Under *Build and deployment* choose **Deploy from a branch**, then select branch `main` and folder `/ (root)`. Click **Save**.
4. After about a minute the site is live at `https://<your-user>.github.io/design-upscaler/`.

## What it does

| Input | Output |
|---|---|
| `.psd` | A new layered PSD enlarged 2–4×. Every pixel layer is AI-enhanced, and so are smart-object images if you tick that option. Positions, masks, vector masks, layer-effect sizes and text are scaled to match. Text stays editable. |
| `.af`, `.afphoto`, `.afdesign` | A ZIP of the enhanced embedded images. In Affinity, select an image, click **Replace Image…** and pick the enhanced file. It keeps the same size and position. |
| `.png`, `.jpg`, `.webp` | The enhanced image. |

**Affinity pixel layers.** Painted or rasterised layers are stored in Affinity's closed format and can't be read in the browser. Export the document from Affinity with **File → Export → PSD** (keep layers on), run the PSD through the page, then open the result in Affinity.

## Free tools used (all MIT-licensed, loaded from jsDelivr)

- [UpscalerJS](https://upscalerjs.com) 1.0.0 with ESRGAN Slim, Medium and Thick models, running on [TensorFlow.js](https://www.tensorflow.org/js) 4.11.0
- [ag-psd](https://github.com/Agamnentzar/ag-psd) 34.1.0 to read and write PSDs
- [fzstd](https://github.com/101arrowz/fzstd) 0.1.1 to read Affinity's compressed blocks
- [JSZip](https://stuk.github.io/jszip/) 3.10.1 to build the ZIP download

## Tips

- **Speed.** The model runs on the GPU through WebGL. A laptop with a decent GPU handles a 1000 px image at 4× in under a minute. Without a GPU it can take several minutes.
- **Large documents.** Each side is limited to 16,000 px in the browser and 30,000 px in a PSD. Use 2× for big files.
- **Quality.** "Maximum" uses ESRGAN Thick, which gives the best detail and is the slowest. "High" is a good everyday choice.
