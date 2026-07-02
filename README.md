# TinyTape

Browser-based editor and Web Bluetooth printer client for small 384 px BLE thermal printers.

The app runs as a static web page. It prepares images/text for a narrow thermal tape, previews the final monochrome raster, and sends the print job directly to the printer over BLE.

## Features

- Print from desktop Chrome without a vendor mobile app.
- Add one or many images to a long tape layout.
- Drag images on the tape and adjust scale/position with sliders.
- Add text blocks and edit them in place: content, font, size, and padding of a selected block.
- Tape length tracks the content automatically; "По содержимому" re-fits it, or the slider adds blank space manually.
- Preview both the editable layout and the final raster that will be sent to the printer.
- Tune dithering, threshold, contrast, heat level, and BLE sending speed.
- Reconnect to the last permitted printer when the browser allows it.
- Filtered Bluetooth picker: only printers show up, not every BLE device nearby.
- Automatic reconnect when the BLE connection drops.
- Battery level in the status bar when the printer exposes the standard battery service.

## Compatibility

Tested with a no-name cat-style BLE thermal printer that is normally used through the iOS app `Fun Print`.

Expected BLE protocol:

- Service: `0000ae30-0000-1000-8000-00805f9b34fb` or `0000af30-0000-1000-8000-00805f9b34fb`
- Write characteristic: `0000ae01-0000-1000-8000-00805f9b34fb`
- Notify characteristic: `0000ae02-0000-1000-8000-00805f9b34fb`
- Print width: `384` px

Other cheap BLE thermal printers may use the same protocol, but this is not guaranteed.

TinyTape is not affiliated with, endorsed by, or connected to Fun Print or any printer vendor.

## Browser Requirements

Use a Chromium browser with Web Bluetooth support:

- Google Chrome
- Microsoft Edge
- Chromium

Safari and Firefox do not support this workflow.

The page must be opened from:

- `https://...`, for example GitHub Pages
- `http://localhost`
- `http://127.0.0.1`

Opening `index.html` directly as a local file is not recommended.

## Run Locally

From this folder:

```bash
python3 -m http.server 8000 --bind 127.0.0.1
```

Open in Chrome:

```text
http://127.0.0.1:8000/
```

On macOS you can also double-click:

```text
start.command
```

It starts the local server and opens Chrome.

## Publish With GitHub Pages

This project does not need a build step.

1. Create a public GitHub repository, for example `tinytape`.
2. Push these files:
   - `index.html`
   - `README.md`
   - `LICENSE`
   - `.gitignore`
   - optionally `start.command`
3. In GitHub, open `Settings -> Pages`.
4. Set source to `Deploy from a branch`.
5. Choose the `main` branch and `/root`.
6. Open the generated `https://<user>.github.io/<repo>/` URL in Chrome.

## Usage

1. Turn on the printer.
2. Make sure it is not connected to the phone app.
3. Open TinyTape in Chrome.
4. Press `Подключить`.
5. Select the printer in the Bluetooth dialog.
6. Add images or text to the tape.
7. Use `Растр` preview to check what will actually print.
8. Press `Печатать`.

For short prints, keep `Режим печати` set to `Быстрый`. If a long print stops after several centimeters, switch to `Надёжный` or `Медленный`.

## Troubleshooting

If the printer does not appear:

- If the picker list is empty, close it and press `Подключить` again: the second attempt lists all Bluetooth devices.
- Turn Bluetooth off/on on the computer.
- Turn the printer off/on.
- Disconnect it from the phone app.
- Reload the page with `Cmd+Shift+R`.
- Open Chrome Bluetooth settings and remove stale permissions if needed.

If printing stops halfway:

- Use `Режим печати -> Надёжный` or `Медленный`.
- Lower the heat level slightly.
- Try a shorter tape first.
- Make sure the battery is charged.

If the page cannot connect automatically:

- This is a browser permission limitation.
- Press `Подключить` and select the printer manually once.
- Chrome may then allow reconnecting through the saved device permission.

## License

MIT
