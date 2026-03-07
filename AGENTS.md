# AGENTS.md — neil-stoddard-photos

This is a Hugo-based photography portfolio site at neilstoddard.com. This file documents the project structure and conventions for adding new photo pages.

---

## Project Structure

```
assets/images/       # Source JPEG image files (processed by Hugo pipeline)
content/highlights/  # All photo content pages, organized by category
  flora/             # Plants, flowers
  fauna/             # Animals
  people/            # Portraits
  place/             # Landscapes, locations
  object/            # Still life, events, abstract
static/              # Verbatim static files (CSS, JS, fonts, logo, favicon)
layouts/             # Site-level overrides of the Eternity theme
hugo.yaml            # Site configuration
```

---

## Adding a New Photo Page

### 1. Image file

Images are exported from Lightroom and placed in `assets/images/` by the user before asking for a page to be created. **Do not rename or move image files.**

New photos use date-based naming (already set at export time):

```
YYYYMMDD-N.jpg    # e.g. 20260304-1.jpg  (date + sequence number for that day)
```

Legacy images used camera naming (DSC_NNNN.jpg, IMG_*.jpg, etc.) — don't use those conventions for new photos.

**Workflow: finding the image to use**

When asked to create a new photo page, run `git status` first to identify untracked files in `assets/images/`. If exactly one new image is present, use it. If multiple new images are present, ask the user which one to create the page for.

### 2. Content file

Create a Markdown file in the appropriate category under `content/highlights/`:

```
content/highlights/flora/my-photo-title.md
```

Use lowercase, hyphenated filenames that match the page title.

### 3. Front matter format

```yaml
---
title: "Page Title"
images:
  - /images/YYYYMMDD-N.jpg
tags:
  - all
  - <category>         # one of: flora, fauna, people, place, object
  - highlights         # optional — include to show on the Highlights page
weight: YYYYMMDDNN     # date + zero-padded 2-digit sequence, e.g. 2026030401
---

Optional caption or description text goes here.
```

### 4. Weight convention

Weight controls sort order (higher weight = appears earlier/more prominently).

- **Date-based images**: `YYYYMMDDNN` — concatenate the date with a zero-padded 2-digit sequence number. Example: `20260304-1.jpg` → weight `2026030401`.
- **Legacy DSC images**: weight is just the DSC number, e.g. `DSC_12102.jpg` → weight `12102`.

### 5. Categories

| Tag | Directory | Use for |
|---|---|---|
| `flora` | `content/highlights/flora/` | Plants, flowers, trees |
| `fauna` | `content/highlights/fauna/` | Animals, birds, insects |
| `people` | `content/highlights/people/` | Portraits, people |
| `place` | `content/highlights/place/` | Landscapes, locations, architecture |
| `object` | `content/highlights/object/` | Still life, events, celestial, abstract |

Always include the `all` tag. Include `highlights` to feature the photo on the main gallery page.

---

## Complete Example

For a photo file `assets/images/20260304-1.jpg`, a flora photo featured in highlights:

```yaml
---
title: "Grape Soda Purple"
images:
  - /images/20260304-1.jpg
tags:
  - all
  - flora
  - highlights
weight: 2026030401
---

Optional caption text describing the photo and its story.
```

---

## Captions

The user will often provide an Instagram (or other social media) post as the source for caption text. Use the narrative body of that post as the page caption. Strip out before saving:

- Camera gear / EXIF lines (EXIF is read automatically from the image file and displayed by the theme)
- Hashtags
- Emoji
- Any other social media formatting

If the user does not provide caption text, ask whether they want one or leave the caption blank.
