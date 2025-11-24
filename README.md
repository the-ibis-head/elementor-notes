# Mastering Elementor

**Time to Read:** ~13 minutes

Elementor has evolved into one of the most powerful visual builders in the WordPress ecosystem. 
This guide delivers a clear, technical path to mastering Elementor.

---

## Local Setup with Valet, WP-CLI & Astra/Elementor

### Install prerequisites (macOS)

```bash
# Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# PHP, MySQL, Mailpit, WP-CLI, Composer
brew install php mysql mailpit wp-cli composer
brew services start mysql
```

- Homebrew: [https://brew.sh](https://brew.sh)
- PHP: [https://formulae.brew.sh/formula/php](https://formulae.brew.sh/formula/php)
- MySQL: [https://formulae.brew.sh/formula/mysql](https://formulae.brew.sh/formula/mysql)
- Mailpit: [https://github.com/axllent/mailpit](https://github.com/axllent/mailpit)
- WP-CLI: [https://wp-cli.org](https://wp-cli.org)
- Composer: [https://getcomposer.org](https://getcomposer.org)

### Install & Configure Laravel Valet

```bash
composer global require laravel/valet
export PATH="$HOME/.config/composer/vendor/bin:$PATH"  # or ~/.composer/vendor/bin
valet install

mkdir -p ~/Sites && cd ~/Sites
valet park
```

- Laravel Valet: [https://laravel.com/docs/valet](https://laravel.com/docs/valet)

### Create a New WordPress Site

```bash
cd ~/Sites
SITE=elementor-site
URL="$SITE.test"
DB=elementor_site

mkdir $SITE && cd $SITE
valet link $SITE

wp core download
wp config create \
  --dbname=$DB --dbuser=root --dbpass="" --dbhost=127.0.0.1
wp db create
wp core install \
  --url="$URL" \
  --title="Elementor Dev Site" \
  --admin_user=admin \
  --admin_password=password \
  --admin_email=you@example.com
```

- WordPress: [https://wordpress.org/download](https://wordpress.org/download)
- Valet Link: [https://laravel.com/docs/valet#the-link-command](https://laravel.com/docs/valet#the-link-command)
- WP-CLI Core: [https://developer.wordpress.org/cli/commands/core](https://developer.wordpress.org/cli/commands/core)

### Create / Reset the Database & Site

```bash
# Create DB (if missing)
wp db create

# Full reset
wp db reset --yes
wp core install \
  --url="$URL" \
  --title="Elementor Dev Site" \
  --admin_user=admin \
  --admin_password=password \
  --admin_email=you@example.com

# Only wipe content
wp site empty --yes
```

- WP-CLI DB: [https://developer.wordpress.org/cli/commands/db](https://developer.wordpress.org/cli/commands/db)
- WP-CLI Site Empty: [https://developer.wordpress.org/cli/commands/site/empty](https://developer.wordpress.org/cli/commands/site/empty)

### Install Astra & Elementor

```bash
wp theme install astra --activate
wp plugin install elementor --activate

# Elementor Pro
# wp plugin install /path/to/elementor-pro.zip --activate
```

- Astra Theme: [https://wpastra.com](https://wpastra.com)
- Elementor: [https://elementor.com](https://elementor.com)
- WP-CLI Theme: [https://developer.wordpress.org/cli/commands/theme](https://developer.wordpress.org/cli/commands/theme)
- WP-CLI Plugin: [https://developer.wordpress.org/cli/commands/plugin](https://developer.wordpress.org/cli/commands/plugin)

### Mailpit for Email Testing

```bash
mailpit
```

- Mailpit Docs: [https://github.com/axllent/mailpit](https://github.com/axllent/mailpit)
- Mailpit SMTP Access: `127.0.0.1:1025`
- Mailpit UI: [localhost:8025](http://localhost:8025)

---

## Free vs Pro Versions

When choosing between **Elementor Free** and **Elementor Pro**, it helps to understand how each version affects your workflow, design flexibility, and site-building capabilities.

### Elementor Free

Elementor Free is ideal for quick builds, small personal sites, or anyone new to visual page builders. It includes:

* Drag-and-drop editor with responsive controls
* 40+ basic widgets (Headings, Text, Images, Buttons, etc.)
* Basic templates and blocks
* Global fonts and colors
* Mobile editing
* Flexbox Container support

### Elementor Pro

Elementor Pro unlocks full site-building power and advanced marketing features. It includes:

* Theme Builder (custom headers, footers, single posts, archives, 404 pages)
* 90+ Pro widgets, including Forms, Slides, Nav Menu, Posts, Loop Builder, and more
* Popup Builder (modals, exit-intent, banners)
* WooCommerce Builder (product templates, shop archives, cart/checkout)
* Advanced Motion Effects (scroll and mouse-based animations)
* Dynamic content integration (ACF, Pods, Meta Box, Toolset)
* Premium templates and kits

| Feature Category                 | Elementor Free | Elementor Pro                       |
| -------------------------------- | -------------- | ----------------------------------- |
| Page Builder                     | Yes            | Yes                                 |
| Basic Widgets                    | 40+            | 40+                                 |
| Pro Widgets                      | No             | 90+                                 |
| Theme Builder                    | No             | Yes                                 |
| Popup Builder                    | No             | Yes                                 |
| WooCommerce Builder              | No             | Yes                                 |
| Loop Builder                     | No             | Yes                                 |
| Forms Widget                     | No             | Yes                                 |
| Dynamic Content                  | No             | Yes                                 |
| Premium Templates                | Limited        | Full Library                        |
| Smooth Workflow for Client Sites | Basic          | Advanced                            |
| Best Use Case                    | Simple sites   | Production-ready, scalable websites |

- Free Plugin [https://elementor.com/products/page-builder-plugin/](https://elementor.com/products/page-builder-plugin/)
- Pro Features [https://elementor.com/pro/](https://elementor.com/pro/)

---

## Rolling Back Elementor Versions

When an Elementor update introduces conflicts or regressions, rolling back to a stable version is a quick way to restore site functionality. Elementor provides built-in rollback tools, and you can also revert via WP-CLI or helper plugins.

### Roll Back from the Elementor Interface

Elementor includes a built-in version control panel.

**Steps:**

1. Go to **WordPress Dashboard → Elementor → Tools → Version Control**
2. Choose a previous version under **Rollback Version**
3. Click **Reinstall**

### Roll Back Using WP-CLI

WP-CLI offers precise control and is ideal for developers working locally or on staging.

```bash
# Roll back Elementor Free
wp plugin install elementor --version=3.18.3 --force

# Roll back Elementor Pro (needs valid license)
wp plugin install elementor-pro --version=3.18.1 --force
```

- [https://elementor.com/help/version-control-rollback/](https://elementor.com/help/version-control-rollback/)
- [https://developer.wordpress.org/cli/commands/plugin/install/](https://developer.wordpress.org/cli/commands/plugin/install/)
- [https://elementor.com/help/how-to-manually-update-elementor-pro/](https://elementor.com/help/how-to-manually-update-elementor-pro/)

---

## Keyboard Shortcuts for Power Users

| Action                   | Shortcut             |
| ------------------------ | -------------------- |
| Show Navigator           | Cmd/Ctrl + I         |
| Finder (search elements) | Cmd/Ctrl + E         |
| Switch Panel ↔ Canvas    | Cmd/Ctrl + P         |
| Undo                     | Cmd/Ctrl + Z         |
| Redo                     | Cmd/Ctrl + Shift + Z |
| Save                     | Cmd/Ctrl + S         |
| Responsive Mode          | Cmd/Ctrl + Shift + M |

- [https://elementor.com/help/keyboard-shortcuts](https://elementor.com/help/keyboard-shortcuts)

---

## Adding and Managing Favorite Widgets in Elementor

Elementor’s **Favorite Widgets** feature helps you speed up page-building by pinning the widgets you use most often. This keeps your workflow focused and your panel uncluttered—especially helpful for large sites or when juggling many widget types.

### How to Add Widgets to Favorites

1. Open any page with the **Elementor Editor**.
2. In the widget panel, **right-click** the widget you want to favorite.
3. Click ***Add to Favorites***.
4. The widget now appears in the **Favorites** category at the top of the panel.

### Popular Widgets to Add to Favorites

A good rule of thumb: favorite anything you touch on *almost every build*—usually headings, text, buttons, images, and your main content/grid widgets.

* **Heading** – For page titles, section headings, and hero text.
* **Text Editor** – Body copy, descriptions, and simple rich text.
* **Image** – Hero images, product photos, and feature graphics.
* **Button** – Primary/secondary calls-to-action, links to forms or key pages.
* **Icon / Icon List** – Bullet lists with icons for features, benefits, or steps.
* **Divider / Spacer** – Quick visual separation and spacing (especially handy when refining layouts).
* **Image Gallery / Image Carousel** – For portfolios, product grids, and image sliders.
* **Video** – Embedded YouTube/Vimeo videos with customizable controls.

### Sync Favorites Between Sites?

Right now, Elementor **does not provide a native way to sync the Favorites list across different sites** (or even across a multisite network). Favorites are stored per site/editor environment.

### Creating a Simple Custom Elementor Widget

Below is a **minimal “Hello World”–style custom widget** as a standalone plugin. It registers a simple widget that just outputs some text. This follows Elementor’s recommended pattern of extending `\Elementor\Widget_Base` and registering via an addon.

Create a new file in `wp-content/plugins/` called `elementor-simple-widget.php`:

```php
<?php
/**
 * Plugin Name: Elementor Simple Widget
 * Description: A minimal custom widget example for Elementor.
 * Author: ThothProcess
 * Version: 1.0.0
 */

if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

// Make sure Elementor is active.
function esw_check_elementor_active() {
	return did_action( 'elementor/loaded' );
}

/**
 * Simple Hello World widget class.
 */
class ESW_Hello_World_Widget extends \Elementor\Widget_Base
{
	public function get_name() {
		return 'esw_hello_world';
	}
	public function get_title() {
		return __( 'ESW Hello World', 'esw' );
	}
	public function get_icon() {
		return 'eicon-editor-bold';
	}
	public function get_categories() {
		// Puts it in the "General" category.
		return [ 'general' ];
	}
	protected function register_controls() {
		$this->start_controls_section(
			'content_section',
			[
				'label' => __( 'Content', 'esw' ),
				'tab'   => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);
		$this->add_control(
			'title',
			[
				'label'       => __( 'Title', 'esw' ),
				'type'        => \Elementor\Controls_Manager::TEXT,
				'default'     => __( 'Hello from a custom widget!', 'esw' ),
				'placeholder' => __( 'Enter your text', 'esw' ),
			]
		);
		$this->end_controls_section();
	}
	protected function render() {
		$settings = $this->get_settings_for_display();
		echo '<div class="esw-hello-world">' . esc_html( $settings['title'] ) . '</div>';
	}
}

/**
 * Register the widget with Elementor.
 */
function esw_register_widgets( $widgets_manager ) {
	if ( ! esw_check_elementor_active() ) {
		return;
	}
	$widgets_manager->register( new \ESW_Hello_World_Widget() );
}

add_action( 'elementor/widgets/register', 'esw_register_widgets' );
```

- [https://developers.elementor.com/docs/widgets/widget-structure/](https://developers.elementor.com/docs/widgets/widget-structure/)
- [https://developers.elementor.com/docs/getting-started/first-addon/](https://developers.elementor.com/docs/getting-started/first-addon/)
- [https://developers.elementor.com/docs/widgets/widget-structure/](https://developers.elementor.com/docs/widgets/widget-structure/)

---

## Setting Global Typography and Styles

Elementor’s global design tools let you define consistent typography across your entire site—headings, body text, buttons, and form elements—all from one place. Using these settings properly helps maintain brand consistency, improve accessibility, and reduce the need for per-widget customization.

### Where to Configure Global Typography

You can manage global typography from:

**Elementor → Site Settings → Typography**

Here you can define:

* **Global Fonts:** Primary, Secondary, Text, and Accent
* **Headings:** H1–H6 font family, weight, size, line height
* **Body text:** Font family, size, weight, line height
* **Theme Style Overrides:** Disable theme typography if needed
* **Custom CSS variables** (Elementor Pro)

Once set, these values automatically apply to all widgets unless manually overridden.

### Using Google Fonts in Elementor

Elementor bundles built-in access to Google Fonts. To use them:

1. Open any widget with typography controls.
2. Under **Style → Typography**, select the **Font Family** dropdown.
3. Search for a Google Font (e.g., “Inter”, “Roboto”, “Poppins”).
4. Apply weights and variations as needed.

### Load Only What You Use

**Elementor → Settings → Advanced → *Load Only Used Google Fonts***

Enabling this prevents Elementor from loading unused font weights/styles, improving performance.

### Enabling Local Google Fonts (GDPR / Privacy)

To keep fonts self-hosted:

**Elementor → Settings → Advanced → Google Fonts → Local**

This downloads fonts to your server, reducing external requests and improving compliance with GDPR.

### Common Typography Issues & Fixes

#### Theme Overrides Elementor Styles

Some WordPress themes apply typography styles that conflict with Elementor.

**Fix:**
Go to *Site Settings → Theme Style* and ensure “Default Colors” and “Default Fonts” are disabled (or adjust theme settings).

#### Fonts Not Loading (Google Fonts Blocked or GDPR)

If fonts aren’t appearing:

* Confirm local font hosting is enabled.
* Clear Elementor + Browser cache.
* Test switching to a system font temporarily.

#### Inconsistent Heading Sizes Across Widgets

Widgets may override global typography due to:

* Manual widget-level typography settings
* Imported templates with embedded styles

**Fix:** Right-click a widget → **Reset Style**, or manually set typography to “Default”.

#### CLS (Cumulative Layout Shift) from Web Fonts

Slow-loading fonts cause text to jump on page load.

**Fixes:**

* Use “swap” font-display (enabled automatically for local fonts).
* Reduce number of font weights.
* Choose system fonts where possible.

### Applying Typography via Custom CSS Variables (Pro)

```css
/* Example: Use global variables from Site Settings */
h1 {
  font-family: var(--e-global-typography-primary-font-family);
  font-size: var(--e-global-typography-primary-font-size);
}
```

- Elementor Site Settings: [https://elementor.com/help/site-settings/](https://elementor.com/help/site-settings/)
- Typography Basics in Elementor: [https://elementor.com/help/typography/](https://elementor.com/help/typography/)
- Google Fonts Documentation: [https://fonts.google.com/](https://fonts.google.com/)
- Elementor Performance Settings: [https://elementor.com/help/performance/](https://elementor.com/help/performance/)

---

## Text Animations & Scroll Effects + GSAP Video Scroll

You can add text animations — typing effects, transitions and scroll-triggered text inside Elementor, and use GSAP for more advanced effects.

### Typing Effects

In Elementor (free or Pro) you can simulate typing text via a few strategies:

Use the **Heading / Text Editor widget** and animate it via entrance animations (fade, typewriter) — some themes/widgets support a “typewriter” effect out of the box (Elementor Pro has a *Text Rotator* or *Animated Headline* widget)

In the Free version create a custom typing CSS class and keyframes, then apply this class via the Advanced → CSS Classes field.

  ```css
  .typing {
    overflow: hidden;
    white-space: nowrap;
    animation: typing 3s steps(30, end), blink-caret .5s step-end infinite;
  }
  @keyframes typing {
    from { width: 0; }
    to { width: 100%; }
  }
  @keyframes blink-caret {
    from, to { border-color: transparent; }
    50% { border-color: black; }
  }
  ```

### Transitions & Entrance Animations

Elementor widgets support entrance animations (fade in, slide in, zoom, etc) and hover/transitions:

- Choose a widget, go to Advanced → Motion Effects → Entrance Animation.
- Use the built-in transitions and delay/stagger options.
- For more control (e.g., split text, letter by letter) you can use the *Animated Headline* (Pro) or add custom JS + GSAP.
  

### Scroll Animations for Text

To animate text on scroll (as the user scrolls the page), Elementor Pro offers **Motion Effects → Scrolling Effects** (vertical/horizontal scroll, transparency, rotate, scale) and **Sticky Effects**.

In the free version, you're more limited: you can use CSS (position: sticky, transform on scroll with IntersectionObserver) or embed custom code. But for more advanced control (like synchronising text with scroll progress, or pinning sections while animating), GSAP becomes the tool of choice.

### What is GSAP and How It Works

The GreenSock Animation Platform (GSAP) is a high-performance JavaScript animation library for the web. It allows you to animate DOM elements or canvases with much more control and performance than typical CSS transitions.

- Elementor gives you UI for typical animations, but GSAP gives next-level: scroll-scrubbed animations, synchronized timelines, video scrubbing, sequence animations, pinned sections.
- You can embed GSAP code in Elementor via HTML widgets, custom JS, or theme/child theme files.
- Works whether you’re on the free or Pro version — the difference is mostly how much UI support Elementor provides, not whether GSAP works.

#### Key Concepts

- **Tween**: Animate one property (e.g., `gsap.to(".box", { x:100, duration:1 })`).
- **Timeline**: Sequence or group tweens (`gsap.timeline()`), enabling complex choreographies.
- **Plugins**: For scroll-based control, GSAP offers `ScrollTrigger`, `ScrollSmoother`, etc.
- **Registration**: You must register plugins:

```js
gsap.registerPlugin(ScrollTrigger);
```

#### How It Works Under the Hood

- You target elements (DOM, canvas) and animate numeric properties over time (or linked to scroll).
- With `ScrollTrigger`, you can **scrub** an animation along with the scrollbar, **pin** sections (freeze while animating), **trigger** when elements enter/exit viewport. 
- Performance optimisations: WebGL/canvas or hardware-accelerated transforms; GSAP takes care of debounce, throttling, etc.

### Implementing a Video Scroll Animation with GSAP in Elementor

Here’s a step-by-step guide that works for both free and Pro Elementor versions.

#### Step 1: Prepare your HTML structure (Elementor)

Add an **HTML widget** (or use Theme/Child theme file) where you want your scroll animation.

```html
<!-- Elementor HTML widget -->
<div class="video-scroll-container">
  <video class="scrollVideo" src="/videos/exploding-watermelon.mp4" muted playsinline></video>
</div>
<div class="scrollSpacer" style="height: 300vh;"></div>

<!-- Set height so the video can scrub while container is pinned -->
<div class="scrollSpacer" style="height: 300vh;"></div>
```

In your Elementor widget’s Advanced → Custom CSS/Classes, add classes like `video‐scroll‐container`.

#### Step 2: Style with CSS

```css
.video-scroll-container {
  position: relative;
  height: 100vh;
  overflow: hidden;
}

.scrollVideo {
  position: sticky;
  top: 0;
  width: 100%;
  height: auto;
}
```

#### Step 3: Load GSAP + ScrollTrigger

In your theme or via an Elementor HTML widget add:

```html
<script src="https://cdn.jsdelivr.net/npm/gsap@3/dist/gsap.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3/dist/ScrollTrigger.min.js"></script>
```

Then in a `<script>` tag:

```js
gsap.registerPlugin(ScrollTrigger);

const video = document.querySelector(".scrollVideo");

gsap.to(video, {
  currentTime: video.duration,    // animate from 0 to end
  ease: "none",
  scrollTrigger: {
    trigger: ".video-scroll-container",
    start: "top top",
    end: "bottom top",
    scrub: true,
    pin: true,
    anticipatePin: 1
  }
});
```

#### Step 4: Handle video loading & duration

Because we animate `currentTime`, ensure the video metadata is loaded before animating:

```js
video.addEventListener("loadedmetadata", function() {
  // Now video.duration is valid
  gsap.to(video, {
    currentTime: video.duration,
    ease: "none",
    scrollTrigger: {
      trigger: ".video-scroll-container",
      start: "top top",
      end: () => "+=" + (video.duration * 100), // adjust scroll length
      scrub: true,
      pin: true
    }
  });
});
```

#### Optimise & test

- Use a short video, compressed and encoded for web (`libx264`, `‐crf 20`, `‐movflags faststart`) as described in the GSAP community. ([GSAP][3])
- Test on mobile — you may choose fallback (static image) for slow devices.
- Preload or hide until ready.

#### Tips & Considerations

- Use a **muted**, **playsinline**, **autoplay** if desired — but for scroll-controlled maybe no autoplay, you scrub manually.
- Ensure the video codec is friendly for scrubbing (lots of keyframes). See GSAP forum discussion about encoding. ([GSAP][3])
- Consider fallback: For devices that don’t support video scrubbing smoothly, show a static image or simplified animation.
- Performance matters: Large video files + high resolution can cause jank.
- Combine text animations + scroll: While your video scrolls, you can overlay text via Elementor (with GSAP or Elementor’s Motion Effects) to reinforce storytelling.

- Watermelon explosion. Super slow motion animation: [https://www.shutterstock.com/video/clip-1053384449-watermelon-explosion-super-slow-motion-animation](https://www.shutterstock.com/video/clip-1053384449-watermelon-explosion-super-slow-motion-animation)
- ScrollTrigger | GSAP: [https://gsap.com/docs/v3/Plugins/ScrollTrigger/](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)
- Video Scroll Animation - GSAP - GreenSock [https://gsap.com/community/forums/topic/32782-video-scroll-animation/](https://gsap.com/community/forums/topic/32782-video-scroll-animation/)





## Integrating Elementor with ACF (Advanced Custom Fields)

Elementor Pro pairs exceptionally well with **Advanced Custom Fields**, enabling fully dynamic, client-friendly, and scalable WordPress builds. This combination allows you to convert WordPress into a true CMS with structured data, reusable templates, and automated content layouts.

This section provides a comprehensive approach to using ACF with Elementor, including field creation, dynamic binding, repeater loops, and advanced relationships.

---

## 11.1 Why Use ACF with Elementor?

ACF adds structured data fields to posts, pages, custom post types, or global options pages. Elementor Pro can *bind* those fields to visual widgets, turning your designed layouts into dynamic templates that automatically update when content changes.

Key benefits include:

* Separation of **content** from **presentation**
* Standardized inputs for non-technical clients
* Centralized repeatable structures (Repeater, Flex Fields)
* Advanced content modeling (Relationships, Post Objects, Taxonomy metadata)
* Highly scalable, template-driven sites

This is essential for real-world WordPress development, especially when working with large editorial teams or content-heavy websites.

---

## 11.2 Creating ACF Fields

1. WordPress Admin → **Custom Fields → Add New**
2. Create a field group, e.g. “Project Details”
3. Add fields such as:

   * **Text** (Project Title)
   * **Image** (Featured Image Override)
   * **Repeater** (Gallery Items)
   * **URL** (External Link)
   * **Select** (Project Type)
4. Assign the field group to a location:

   * Post Type = Projects
   * Or specific pages, taxonomies, options, etc.

Save the group.

---

## 11.3 Binding ACF Fields Inside Elementor

Elementor Pro widgets feature a **Dynamic Tags** icon beside key input fields.

Examples:

### Text Binding

Example: Title widget → Title → Dynamic Tags → ACF Field → “project_title”

### Image Binding

Image widget → Image → Dynamic Tags → ACF Image

### URL Binding

Button → Link field → Dynamic Tags → ACF URL

### Choosing Format

Each tag supports formatting such as:

* Raw text
* Link URL
* Image ID
* Image URL
* Array → converted to human-readable output

---

## 11.4 Using ACF with Elementor Theme Builder

To build dynamic site templates:

1. Templates → **Theme Builder → Single**
2. Create a template for your CPT (e.g., Projects)
3. Insert widgets and bind fields using Dynamic Tags:

   * Dynamic title
   * Dynamic featured image or ACF image
   * Dynamic repeater content
   * Dynamic buttons linking to project URLs

Publish conditions:

* **Include → Projects → All**
  or
* Select specific taxonomies.

This is the cornerstone of scalable Elementor + ACF development.

---

## 11.5 Repeater Fields in Elementor

Elementor Pro includes the **Loop Builder**, enabling dynamic repeaters.

### Using Repeater Fields via Loop Builder

1. Templates → **Loop Item**
2. Design an item card (image, title, fields)
3. Bind all widgets to ACF repeater subfields
4. Use a Loop Grid widget to display the collection

Example ACF repeater:

* gallery_items (Repeater)

  * gallery_image (Image)
  * gallery_caption (Text)

Bind in Elementor:

* Image widget → Dynamic Tag → ACF Sub Field → gallery_image
* Text widget → Dynamic Tag → ACF Sub Field → gallery_caption

Elementor will render each repeater row automatically.

---

## 11.6 ACF Relationship and Post Object Fields

Elementor can render related posts using:

* Loop Grid
* Post widget (Pro)
* Dynamic fields inside a template

Example: ACF field “related_projects” returns array of post IDs.

Process:

1. Create a Loop Item template for related posts
2. Bind post data to Dynamic Tags
3. Use Loop Grid → Source → ACF Relationship Field
4. Choose the ACF field name (“related_projects”)

---

## 11.7 ACF Flexible Content with Elementor

Flexible Content is like a structured block editor inside ACF.

Option 1:
Use multiple Elementor Loop Item templates and switch based on the layout selected in ACF.

Option 2:
Use a child theme with conditional template loading:

```php
if( have_rows('flex_sections') ):
    while( have_rows('flex_sections') ): the_row();
        if( get_row_layout() == 'hero_section' ):
            get_template_part('flex/hero');
        elseif( get_row_layout() == 'gallery_section' ):
            get_template_part('flex/gallery');
        endif;
    endwhile;
endif;
```

This gives a hybrid model where Elementor handles design and PHP handles layout logic.

---

## 11.8 ACF Options Pages with Elementor

Options pages allow global content such as:

* Company information
* Footer data
* Header CTAs
* Site-wide notifications

ACF Pro example:

```php
if( function_exists('acf_add_options_page') ) {
    acf_add_options_page([
        'page_title' => 'Site Settings',
        'menu_title' => 'Site Settings',
        'menu_slug'  => 'site-settings'
    ]);
}
```

Elementor binding:
Dynamic Tags → ACF Options → Select your global field

Use this for:

* Global contact details
* Global hero content
* Dynamic footer content
* Company address, emails, etc.

---

## 11.9 ACF + Elementor Query Filters (Advanced)

Elementor supports custom PHP-based query filters. This allows you to modify the Loop Grid query using ACF metadata conditions.

Example: Only show posts with meta key `featured` = true.

```php
add_action('elementor/query/featured_projects', function($query) {
    $query->set('meta_key', 'featured');
    $query->set('meta_value', '1');
});
```

Use in Elementor:
Loop Grid → Query → Custom Query ID → `featured_projects`

---

## 11.10 Security, Performance, and Best Practices

* Always sanitize ACF output with `esc_html()`, `wp_kses()`, or type restrictions.

* Use lazy loading for ACF images via Elementor’s settings.

* Avoid storing large datasets in single ACF fields; use CPTs instead.

* Set a naming convention for fields:

  * `project_title`
  * `project_gallery_image`
  * `company_phone`

* Keep ACF JSON sync enabled for version-controlled environments (`acf-json` folder).

---

## 11.11 When to Use ACF vs. Elementor Native Fields

Use **ACF** when:

* You need structured, validated data
* Editors require predictable fields
* You need CPT relationships, taxonomies, or flexible content
* You are building directory sites, catalogs, or large content systems

Use **Elementor** native content when:

* Data is visual and localized
* Only one editor will manage content
* No relational data is required

---

# Conclusion

Mastering Elementor is fundamentally about mastering process—not just design. With a fast, automated dev environment powered by Laravel Valet, WP-CLI, and modern theme frameworks like Astra, you can build, test, rollback, version, and customize Elementor projects with speed and confidence.
