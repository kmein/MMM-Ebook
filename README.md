# Mr. Money Mustache, as an ebook

**The ebook is regenerated weekly with new posts by a GitHub Action and published to the [latest release](https://github.com/kmein/MMM-Ebook/releases/tag/ebooks).**

### [⬇ Download mmm.epub](https://github.com/kmein/MMM-Ebook/releases/download/ebooks/mmm.epub)

Every post from [Mr. Money Mustache](https://www.mrmoneymustache.com/), oldest to newest, with the images from the blog.

This is a fork of [Jon-Schneider/MMM-Ebook](https://github.com/Jon-Schneider/MMM-Ebook), itself a fork of [beege/MMM-Ebook](https://github.com/beege/MMM-Ebook) updated to use Python 3, to generate the ebooks itself instead of making you do it by hand in Calibre, and to include the images hosted at mrmoneymustache.com.

`generate-ebooks.py` pulls the list of posts from the blog's RSS feed, downloads the pages and images it has not cached locally, and writes the ePub plus the plain HTML it is built from. Calibre converts to mobi, azw3, PDF and the rest from that HTML if you want another format.

### Use

This project depends on:

- **Python 3.10 or newer**, plus the packages in `requirements.txt`.
- **Calibre**, for its `ebook-convert` command. Install it manually or via your package manager — [calibre-ebook.com](https://calibre-ebook.com/). Without it the script still produces the HTML edition, but `Ebooks/mmm.epub` is left untouched.

In the repo root:

```sh
pip3 install -r requirements.txt
./generate-ebooks.py
```

When the script finishes, `Ebooks/mmm.epub` holds the latest posts. That directory is not tracked in git - the published copy lives in the release, so a weekly rebuild does not add 50 MB of binaries to the repository every time.

Scraped feed pages and images are cached in `.cached/` (untracked), so later runs only fetch what is new. Delete that directory to force a full re-scrape.

If you would rather build the book yourself in Calibre, import `import_index.html_in_this_folder_in_calibre_to_create_ebook/index.html` and convert it to whatever format you like. Set Calibre to import HTML files in breadth-first order first, under Preferences → Advanced → Plugins → File type → HTML to ZIP, by checking **Add linked files in breadth first order**.

### Automation

[`.github/workflows/main.yml`](.github/workflows/main.yml) reruns the script every Sunday at 06:00 UTC and uploads the ePub to the `ebooks` release, replacing the previous asset. The download link above always points at that release, so it never goes stale. You can also start a run by hand from the Actions tab (*Regenerate Ebooks* → *Run workflow*). Note that GitHub disables Actions on a freshly forked repository, and suspends scheduled workflows in a repository that has seen no activity for 60 days — if you fork this, enable Actions in your fork.

### MMM Approved!

Mr. Money Mustache endorsed the original version of this project [here](https://forum.mrmoneymustache.com/welcome-to-the-forum/making-a-mr-money-mustache-ebook/).

"Awesome work!! You hereby have my full approval to share this book (and work together to improve it if you like). As long as you give it away for free!"
