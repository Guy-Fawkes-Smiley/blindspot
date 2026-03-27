# BLINDSPOT — Face Redactor

**A free, private, browser-based face redaction. Your photos never leave your device.**

## What it does

Upload a photo. BLINDSPOT finds every face and redacts it — black box, blur, or pixelate. Download the result. Done.

No account. No upload. No server. Free.

## Why it's private

The photo never leaves your browser tab. Face detection runs entirely in WebAssembly on your device, using a locally-executed AI model. The original image is never transmitted anywhere.

**You can verify it yourself:**

1. Open DevTools before you do anything: `F12` on Windows/Linux, `⌘⌥I` on Mac
2. Go to the Network tab
3. Upload a photo and watch what gets sent
4. You will see the model weights load once from jsDelivr CDN. That's it. No image data. Ever.

All source code is readable: `Ctrl+U` / `⌘U` → View Source. No obfuscation.

## Works offline

Download the page once. Disconnect from the internet. It still works.

```
File → Save Page As → Webpage, Complete
```

Open the saved file from your hard drive with Wi-Fi off. The original photo stays on your device because there is no server to send it to.

## Redaction styles

- **Black box** — solid fill, maximum coverage
- **Blur** — downsample/upsample blur, no CSS filter
- **Pixelate** — block mosaic

## Technical details

- Face detection: [@vladmandic/face-api](https://github.com/vladmandic/face-api) (MIT License)
- Model: SSD MobileNet v1 — chosen for accuracy on group photos over faster but less reliable alternatives
- Model weights: ~6MB, loaded once from jsDelivr CDN, cached by browser after first use
- Detection runs on a downsampled canvas for speed; bounding boxes are remapped to full resolution for output
- Output: JPEG, 93% quality, generated as a local blob URL — never touches a server

## Who this is for

Anyone who needs to share a photo but wants to protect the people in it — journalists, researchers, activists, anyone posting group photos publicly who wants to respect the privacy of people who didn't consent to being identified online.

## What this is not

This is not a guarantee of anonymity. It redacts faces detected by the model. The model may miss faces that are obscured, angled, very small, or poorly lit. Check your output before publishing.

## No tracking, no analytics, no cookies, no accounts, no data retention

There is nothing to retain. The tool has no backend.

## License

MIT — read it, fork it, audit it, host your own copy.
