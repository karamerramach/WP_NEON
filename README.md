# Vector Arcade

**A bilingual, responsive WordPress theme with an arcade-inspired neon vector design.**

Vector Arcade is a portfolio and publishing theme built around a dark interface, luminous cyan/magenta/violet accents, geometric line work, and an original SVG arcade illustration. It is designed to make a strong visual impression while keeping the implementation lightweight and understandable: WordPress handles content and routing, PHP templates render the pages, CSS defines the visual system, and a small vanilla-JavaScript file controls mobile navigation.

The project includes an installable WordPress theme and a separate static browser demo. The static demo presents the design and its main sections without requiring a running WordPress installation; it is a showcase of the visual direction, not a WordPress emulator.

## Design and user experience

- **Visual identity:** near-black/navy surfaces, neon cyan and pink highlights, violet accents, subtle grid effects, luminous borders, and bold display typography.
- **Original artwork:** a locally bundled, scalable SVG illustration; no remote image service is required.
- **Responsive layout:** fluid content widths and layouts that adapt across desktop, tablet, and mobile breakpoints.
- **Navigation:** primary and footer menu locations, a useful fallback menu when no primary menu is assigned, and a compact mobile menu.
- **Publishing layouts:** dedicated views for the front page, posts index, individual posts, pages, archives, search results, and 404 responses.
- **Content presentation:** featured-image post cards, post metadata, excerpts, comments, and a footer widget area.
- **Customization:** site identity and logo support, plus Customizer fields for the homepage hero text and primary link.
- **Bilingual interface:** an English/French selector with a persistent visitor preference and a French translation catalog.

## How it is built

### WordPress and PHP

The installable theme is a **classic PHP-template theme**, not a Full Site Editing theme. It follows the WordPress template hierarchy and uses standard WordPress APIs rather than introducing a separate application framework.

`functions.php` contains theme setup and integration code: theme supports, menu registration, image sizes, asset enqueuing, the footer widget area, Customizer controls, language selection, and small template helpers. The templates use the WordPress Loop and core template functions to render posts, pages, categories, search results, comments, and empty/error states.

### Template structure

| File | Responsibility |
|---|---|
| `front-page.php` | Theme landing page and feature showcase |
| `home.php` | Posts index |
| `single.php` | Individual post view |
| `page.php` | Static page view |
| `archive.php` | Category, tag, date, and other archive listings |
| `search.php` | Search results |
| `index.php` | Fallback template |
| `404.php` | Not-found page |
| `header.php`, `footer.php` | Shared site chrome and navigation |
| `comments.php` | Comment display and form integration |
| `template-parts/content-card.php` | Reusable post-card markup |

### Styling and design tokens

`style.css` contains the theme's layout and component styling. Reusable CSS custom properties define the core palette, surfaces, typography, borders, radii, content width, and neon glow effects. Responsive behavior is implemented with CSS media queries; motion-sensitive effects account for `prefers-reduced-motion`.

`theme.json` (schema version 2) declares the editor color palette, typography presets, layout widths, spacing units, and global styles. This gives the block editor a palette and typography that are consistent with the front end. The theme supports WordPress block styles, wide alignment, responsive embeds, and editor styles, but it does not provide custom Gutenberg blocks or the HTML template parts required for a Full Site Editing theme.

The theme uses system font stacks rather than downloading web fonts. Its hero artwork is stored in `assets/images/neon-arcade.svg` and referenced locally.

### JavaScript

`assets/js/navigation.js` is dependency-free vanilla JavaScript. It toggles the mobile navigation, updates `aria-expanded`, closes the menu after a navigation selection, supports Escape to close, and resets the menu state when the viewport returns to desktop width. There is no jQuery, React runtime, bundler, or frontend framework in the theme.

### English and French localization

The theme uses the `vector-arcade` gettext text domain. Translation source files are kept in `languages/`:

- `vector-arcade.pot` — translation template.
- `fr_FR.po` — editable French translation source.
- `fr_FR.mo` — compiled French catalog loaded by WordPress.

The header language selector accepts the `va_lang` query parameter, validates the requested language against the supported `en` and `fr` values, and stores an explicit choice in a first-party cookie. On front-end requests, the theme filters the locale so WordPress and theme gettext strings use the selected English or French catalog. The selector preserves the current page URL when switching languages.

This translates interface strings, not editorial content. Posts, pages, manually named menus, and text saved in Customizer fields still need their own translated versions. A multilingual content plugin such as Polylang or WPML can be used when translated content and language-specific URLs are required.

## Project layout

```text
vector-arcade/
├── assets/
│   ├── images/neon-arcade.svg
│   └── js/navigation.js
├── languages/
│   ├── fr_FR.mo
│   ├── fr_FR.po
│   └── vector-arcade.pot
├── template-parts/content-card.php
├── 404.php
├── archive.php
├── comments.php
├── footer.php
├── front-page.php
├── functions.php
├── header.php
├── home.php
├── index.php
├── page.php
├── search.php
├── single.php
├── style.css
├── theme.json
└── editor-style.css
```

The repository's `index.html` and `style.css` at the demo root form the standalone bilingual preview. The `vector-arcade.zip` file contains the installable WordPress theme.

## Requirements and implementation notes

- WordPress 6.2 or newer (theme header requirement).
- PHP 7.4 or newer (theme header requirement).
- No external font, image, CSS, or JavaScript CDN dependency.
- No theme build or asset-compilation step.
- GPL-2.0-or-later license.

The PHP templates and theme configuration have been prepared for WordPress conventions, and the PHP files have been syntax-checked. A full integration pass against a live WordPress installation and a compatibility matrix across WordPress/PHP versions have not yet been completed. The theme should be treated as a portfolio project under active verification, not as a production-certified release.

## License

Theme code and original artwork are provided under **GPL-2.0-or-later**.
