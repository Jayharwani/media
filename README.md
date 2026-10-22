# media

Large media for [jayharwani.com](https://jayharwani.com), served from GitHub
Pages rather than from the site's own host.

## Why this exists

The site runs on Cloudflare Workers static assets, which do not serve HTTP
byte ranges: a `Range` request comes back `200` with the whole file. A video
player needs ranges to seek, so dragging the scrubber forward past whatever
had buffered simply never resolved — measured at every connection speed from
unthrottled down to 3 Mbps. GitHub Pages returns `206 Partial Content`, so
seeking works.

| file | what it is |
| --- | --- |
| `jay-60.mp4` | the 60-second film, 1920x1080, for landscape screens |
| `jay-60-tall.mp4` | the same minute re-cut 1080x1920, for phones held upright |

Both are H.264 + AAC, 60fps, faststart (moov before mdat, so they stream from
the first byte), two-pass at ~3 Mbps.

`.nojekyll` is here so Pages serves the files directly instead of running them
through Jekyll.
