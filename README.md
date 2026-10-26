# tonyvideo.co

Source for [tonyvideo.co](https://tonyvideo.co), a portfolio of motion design, 3D animation and video editing
published under the name tonymode.

Plain HTML, CSS and JavaScript with no framework or build step, hosted on GitHub Pages.

## Details

The design is based on a video editing timeline. As you scroll, a playhead moves across the top of the page
and a timecode counts up, like scrubbing through a one minute clip.

The background at the top plays one of five short video loops, picked at random and never the same twice in a
row. With reduced motion or data saver turned on, a still image is shown instead.

Videos in the work section open in a player on the page. YouTube isn't loaded until play is pressed, which keeps
the page fast.

## Files

```
index.html       the whole site
css/style.css    styles
js/main.js       video loops, timeline, filters, player
assets/loops/    background loops and their still frames
assets/thumbs/   video thumbnails
assets/img/      favicon and link preview image
```

## Adding a video

1. Make a 960x540 thumbnail:
   `convert thumb.jpg -resize 960x540 -quality 78 assets/thumbs/<name>.webp`
2. Copy one of the `<li class="card">` blocks in `index.html` and change:
   - `data-id` to the YouTube video ID. Unlisted videos work fine.
   - `data-cat` to one or more of `product`, `motion`, `social`, `sports`. These power the filter buttons.
   - The link, thumbnail, title and description.
3. To make it the big featured tile, move the `card--feature` class onto it.

## Adding a background loop

Compress it first so the page stays light:

```
ffmpeg -i in.mp4 -an -vf "scale=1280:-2,fps=30,format=yuv420p" -c:v libx264 -preset slow -crf 30 -movflags +faststart assets/loops/loop-6.mp4
ffmpeg -ss 1 -i assets/loops/loop-6.mp4 -frames:v 1 -q:v 5 assets/loops/loop-6.jpg
```

Then raise `LOOPS` in `js/main.js` by one.

## Running locally

```
python3 -m http.server 8000
```

## License

The code (HTML, CSS and JavaScript) is MIT licensed. The videos, thumbnails, loops and other media are not; see [LICENSE](LICENSE).
