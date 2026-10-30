# OneTapLasPiñas - Image Usage Details

## Project Overview
An NFC smart card web application that displays personal/business information with customizable images.

## Permanent Image Configuration

The `IMAGES` object in `index.html` (lines 397-403) defines default images:

```javascript
const IMAGES = {
  logo: "profile.png",           // Default logo on NFC card
  p1: "product/1.png",           // Product gallery image 1
  p2: "product/2.png",           // Product gallery image 2
  p3: "product/3.png",           // Product gallery image 3
  p4: "product/4.png",           // Product gallery image 4
};
```

## Image Locations & Uses

| Image | Path | Usage |
|-------|------|-------|
| **NFC Background** | `image.png` | Background of the NFC card element (CSS `url("image.png")`) |
| **Logo** | `profile.png` | Default logo displayed on the NFC card; replaceable by user |
| **Product 1** | `product/1.png` | Gallery tile 1 |
| **Product 2** | `product/2.png` | Gallery tile 2 |
| **Product 3** | `product/3.png` | Gallery tile 3 |
| **Product 4** | `product/4.png` | Gallery tile 4 |

## Dynamic Image Workflow

1. **User upload** → Click gallery tile → File input → `FileReader` → Canvas resize → `localStorage`
2. **Storage key**: `onetap-images` (JSON object)
3. **Priority**: `saved[k]` (user upload) → `IMAGES[k]` (default) → `""` (empty)
4. **Display**: `paint()` function toggles `has` class and prepends `<img>` element

## Image Handling Features

- **Resizing**: Max 800px dimension, quality 0.82 JPEG
- **Removal**: × button deletes from `localStorage` and re-renders
- **Fallback**: Default images shown if no user upload exists
- **Supported**: Any image type via `<input accept="image/*">`

## File Structure

```
projectaira/
├── image.png          # NFC card background
├── profile.png        # Default logo
├── index.html         # Main HTML + JS (image config + handling)
├── faq/
│   └── 3 JPG images
├── product/
│   └── 4 PNG images   # Gallery defaults
├── manifest.json
├── sw.js              # Service worker
└── vercel.json
```