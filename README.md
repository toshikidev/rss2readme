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
* [Re @vim_tricks If I may ask a off track question out of the vim part, what is the keyboard input recording application/program used throughout the ani...](https://twitter.com/andatoshiki/status/1673403983506083843)
* [Re @daboigbae Well nothing to do with me even if the description fits, cuz I work with rust. 😝](https://twitter.com/andatoshiki/status/1673401878070304768)
* [好想谈恋爱](https://twitter.com/andatoshiki/status/1659881240311529473)
* [Re @Terraria_Logic happy birthday](https://twitter.com/andatoshiki/status/1658886856057180160)
* [Re @Notepad_plus True](https://twitter.com/andatoshiki/status/1645338285261172736)
<!--END_SECTION:example-->

> This started as a little proof-of-concept for @brianlovin!
