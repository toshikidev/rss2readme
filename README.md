# 📡📝 RSS2README Action
> A GitHub Action that updates a section of a README from an RSS feed.

## Usage

You can use this action in a workflow file like any other:

```yml
name: Update this repo's README

on:
  schedule:
    # Once a day at 8 AM
    - cron: 0 8 * * *

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: toshikidev/rss2readme@latest
        with:
          feed-url: https://jasonet.co/rss.xml
          readme-section: feed
```

### Options

#### `feed-url`:

The URL to an RSS feed. It's assumed that the RSS feed follow the standard format!

#### `readme-section`:

The name of the section of your README to update. This uses [`JasonEtco/readme-box`](https://github.com/JasonEtco/readme-box) to replace a section of the README and update the file. Your README should contain HTML comments like this, where `feed` is the the value of `readme-section`:

```html
### Example RSS feed:

<!--START_SECTION:feed-->
...
<!--END_SECTION:feed-->
```

You can inspect this repo's README to see it in use!

#### `empty-commits`: (default: true)

Set this to `false` to not commit anything when this action run but the section didn't change.

#### `max` (default: 5)

The maximum number of items to show from the RSS feed. Defaults to `5`!

#### `template` (default: `"* [{{ title }}]({{ link }}))"`)

You can provide a [Mustache](https://github.com/janl/mustache.js) template to use when rendering each item in the feed. These will be joined by a newline (`\n`). For example:

```yaml
- uses: toshikidev/rss2readme@latest
  with:
    feed-url: https://jasonet.co/rss.xml
    template: "> {{ excerpt }}\n\n[Read more!]({{ url }})"
```

#### `branch` (default: github.repository.default_branch)

You can provide the target branch to update instead of the default.

#### `path` (default: 'README.md')

Path to the README file to update.

### Example RSS feed:

<!--START_SECTION:example-->
* [Re @MIT_CSAIL @Prathkum @SaveToNotion #tweet](https://twitter.com/andatoshiki/status/1643737707926159360)
* [Re @rebecca_hoshino https://t.co/x1Nu8HcG3A](https://twitter.com/andatoshiki/status/1643210118077763586)
* [Re @linuxopsys @SaveToNotion #tweet](https://twitter.com/andatoshiki/status/1643209761998135298)
* [Verifying myself: I am toshikidev on http://Keybase.io. pQuYoKO8oET7dLOazltqkPLQs2MIceG5rr3m / https://keybase.io/toshikidev/sigs/pQuYoKO8oET7dLOazltq...](https://twitter.com/andatoshiki/status/1640183615249346560)
* [Sakura 🌸 https://t.co/YoEmRMTmr3](https://twitter.com/andatoshiki/status/1639967758782812161)
<!--END_SECTION:example-->

> This started as a little proof-of-concept for @brianlovin!
