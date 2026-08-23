# Ford Fight Lab — How to Edit Your Site

Your whole site lives in this GitHub repository. Edit a file, save it, and the live
site updates itself in about a minute. No servers, no uploads, no asking anyone.

## The one workflow you need

1. Go to the repo on github.com and click the file you want (e.g. `fights.html`)
2. Click the **pencil icon** (top right of the file view)
3. Make your edit
4. Click **Commit changes** (the green button)
5. Wait ~1 minute, refresh the live site. Done.

## The pages

| File | What it is |
|---|---|
| `index.html` | Home page |
| `styles.html` | Fighting styles breakdowns |
| `fighters.html` | Fighter profiles |
| `fights.html` | Fight history (with videos) |
| `podcast.html` | Podcast episodes |
| `css/style.css` | Colors and design (edit the `:root` colors at the top to re-theme everything) |

## Adding content — it's all copy-paste

Every page is built from repeating **card blocks**. To add a fighter, a fight, a
style, or an episode: copy an existing block from `<div class="card">` down to its
closing `</div>`, paste it below, and rewrite the text. Each page has a comment
near the top showing you exactly which block to copy.

## Videos (fights page)

Find the fight on YouTube. Copy the part of the URL after `watch?v=` — that's the
VIDEO ID. Inside the card, add:

```html
<div class="video"><iframe src="https://www.youtube.com/embed/VIDEO_ID" title="Fight video" allowfullscreen></iframe></div>
```

That gives you an inline player. (Always embed from YouTube — never upload fight
footage yourself; embedding is allowed, re-uploading isn't.)

## Links to articles or anything else

Two options, use them anywhere:

```html
<!-- a button-style link -->
<a class="watch" href="https://example.com/article" target="_blank" rel="noopener">Read the story</a>

<!-- a normal link inside a sentence -->
<p>As <a href="https://example.com" target="_blank" rel="noopener">this breakdown</a> shows...</p>
```

## Podcast episodes

1. Upload the episode at [creators.spotify.com](https://creators.spotify.com) (free)
2. On the episode: **Share → Embed**, copy the iframe code
3. In `podcast.html`, copy the episode card, update the title/description, and paste
   the iframe where the comment says

Spotify for Creators also pushes your show to Spotify and Apple Podcasts for you.

## Rules of thumb

- Edit one thing at a time and check the live site — easy to spot mistakes that way
- If a page ever looks broken, you probably deleted a `</div>` — check your last commit
  (the repo's **History** button shows every change, and anything can be undone)
- Facts matter in the lab: check records and dates before you publish them
