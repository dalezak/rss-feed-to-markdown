# RSS Feed to Markdown

This GitHub Action converts RSS feed entries to Markdown files. It fetches the RSS feed, extracts relevant information from each entry, and generates Markdown files using a provided template.

## Input Variables

- `feed_url` (required): The URL of the RSS feed.
- `template_file` (required): The path to the template file.
- `output_dir` (required): The directory where the generated Markdown files will be saved.

## Example Usage

```yaml
name: RSS Feed to Markdown

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  convert_feeds:
    runs-on: ubuntu-latest

    steps:
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '16'

      - name: Checkout code
        uses: actions/checkout@v2

      - name: Run RSS Feed to Markdown Action
        uses: keiranlovett/rss-feed-to-markdown@main
        with:
          feed_url: 'https://www.youtube.com/feeds/videos.xml?channel_id=UCuVczNc74_jsmgNlAhHbz-Q'
          template_file: 'assets/template.md'
          output_dir: '_posts/events/'
```

## Template File

1. Create a new Markdown file named template.md.
2. Customize the template to fit your desired output format. You can use Markdown syntax and add placeholders for dynamic content.
3. Identify the parts of the template that you want to be replaced with actual values from the RSS feed entries. Placeholders include `[ID]`, `[DATE]`, `[LINK]`, `[TITLE]`, `[DESCRIPTION]`, `[CONTENT]`, `[MARKDOWN]`, `[AUTHOR]`, `[VIDEO]`, `[IMAGE]`, `[IMAGES]`, `[CATEGORIES]`, `[VIEWS]`, `[RATING]`.
4. Replace the corresponding parts in the template with the desired placeholders. For example:

```markdown
---
id: [ID]
link: [LINK]
title: [TITLE]
date: [DATE]
author: [AUTHOR]
keywords: [CATEGORIES]
image: [IMAGE]
images: [IMAGES]
description: >
  [DESCRIPTION]
---
# [TITLE]
##### [AUTHOR]
_[DATE]_

[MARKDOWN]
```

Make sure to use meaningful placeholders that align with the content you want to display in the generated Markdown files. These placeholders will be replaced with the actual values from the RSS feed entries during the conversion process.

Feel free to adjust the template according to your needs, including adding more metadata or formatting options. The template allows you to control the structure and appearance of the generated Markdown files.

## Compile Project

To package the project, you'll need to use [vercel/ncc](https://github.com/vercel/ncc) which compiles all source code and dependencies into a single file.

```bash
npm i -g @vercel/ncc
```

```bash
ncc build index.js -o dist
```

## Contribution

Feel free to customize the workflow and inputs based on your specific use case.

If you have any questions or need further assistance, please let me know!
