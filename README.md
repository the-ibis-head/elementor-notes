# Elementor
> Compiled notes on elementor

Elementor has evolved into one of the most powerful visual builders in the WordPress ecosystem. 
This guide delivers a clear, technical path to mastering Elementor.

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

- ScrollTrigger | GSAP: [https://gsap.com/docs/v3/Plugins/ScrollTrigger/](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)
- Video Scroll Animation - GSAP - GreenSock [https://gsap.com/community/forums/topic/32782-video-scroll-animation/](https://gsap.com/community/forums/topic/32782-video-scroll-animation/)
- Watermelon explosion. Super slow motion animation: [https://www.shutterstock.com/video/clip-1053384449-watermelon-explosion-super-slow-motion-animation]

#### <ins>Step 1: Prepare your HTML structure (Elementor)</ins>

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

In your Elementor widget’s **Advanced → Custom CSS/Classes**, add classes like `video‐scroll‐container`.

#### <ins>Step 2: Style with CSS</ins>

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

#### <ins>Step 3: Load GSAP + ScrollTrigger</ins>

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

#### <ins>Step 4: Handle video loading & duration</ins>

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

#### <ins>Optimise & test</ins>

- Use a short video, compressed and encoded for web (`libx264`, `‐crf 20`, `‐movflags faststart`) as described in the GSAP community.
- Test on mobile — you may choose fallback (static image) for slow devices.
- Preload or hide until ready.

#### <ins>Tips & Considerations</ins>

- Use a **muted**, **playsinline**, **autoplay** if desired — but for scroll-controlled maybe no autoplay, you scrub manually.
- Ensure the video codec is friendly for scrubbing (lots of keyframes). See GSAP forum discussion about encoding.
- Consider fallback: For devices that don’t support video scrubbing smoothly, show a static image or simplified animation.
- Performance matters: Large video files + high resolution can cause jank.
- Combine text animations + scroll: While your video scrolls, you can overlay text via Elementor (with GSAP or Elementor’s Motion Effects) to reinforce storytelling.

---

## Integrating WooCommerce with Elementor

Elementor works seamlessly with WooCommerce, allowing you to design product pages, archive layouts, and checkout flows using a visual builder instead of relying on theme defaults. 

### Using Elementor to Design WooCommerce Product Pages

Elementor Pro gives you access to dynamic WooCommerce widgets and lets you build fully custom product templates.

**Steps:**

1. Go to **Templates → Theme Builder → Single Product**.
2. Choose **Add New** → *Single Product*.
3. Insert WooCommerce widgets such as:

   * Product Title
   * Product Price
   * Product Image
   * Product Rating
   * Add to Cart
   * Product Meta
   * Product Data Tabs
     
4. Publish and assign the template to **All Products** or a specific product/category.

### Styling or Replacing the Quantity Input**

Many stores want a cleaner or custom-styled quantity field.

#### <ins>Style via Elementor Custom CSS (Pro)</ins>

Add to the **Add to Cart** widget → *Advanced → Custom CSS*:

```css
.woocommerce .quantity input.qty {
  width: 70px;
  padding: 8px;
  border: 2px solid #ddd;
  border-radius: 6px;
  font-size: 16px;
}
```

- [WooCommerce Quantity Docs](https://woocommerce.com/document/template-structure/)

### Editing WooCommerce Product Description Tabs

You can visually style the **Product Data Tabs** widget in Elementor, but if you want to rename or remove tabs:

#### <ins>Rename Tabs</ins>

```php
add_filter( 'woocommerce_product_tabs', function( $tabs ) {
    $tabs['description']['title'] = 'Details';
    $tabs['additional_information']['title'] = 'Specs';
    return $tabs;
});
```

#### <ins>Remove Tabs</ins>

```php
add_filter( 'woocommerce_product_tabs', function( $tabs ) {
    unset( $tabs['reviews'] ); // hides Reviews tab
    return $tabs;
});
```

- [WooCommerce Tabs Filter](https://woocommerce.com/document/editing-product-data-tabs/)

### Enabling PayPal Payments in WooCommerce

WooCommerce supports PayPal via the official **“WooCommerce PayPal Payments”** plugin.

**Install the plugin:**

1. Go to **Plugins → Add New**.
2. Search **WooCommerce PayPal Payments**.
3. Install & activate.
4. Open **WooCommerce → Settings → Payments → PayPal**.

- [PayPal Payments Plugin](https://woocommerce.com/products/woocommerce-paypal-payments/)

### Setting Up PayPal Sandbox Mode for Testing

Sandbox mode lets you test transactions without real money.

#### <ins>Steps to Create PayPal Sandbox Accounts</ins>

1. Visit: [https://developer.paypal.com](https://developer.paypal.com)
2. Log in with your PayPal account.
3. Go to **Dashboard → Sandbox → Accounts**.
4. Create:

   * **Business account** (merchant)
   * **Personal account** (buyer)

#### **Configure Sandbox in WooCommerce**

Inside **WooCommerce → Settings → Payments → PayPal**:

1. Toggle **Enable Sandbox**.
2. Enter your **Sandbox API Credentials**:

   * Sandbox Client ID
   * Sandbox Secret
     
3. Save changes.
4. Test a checkout using your **sandbox personal account** email/password.

- [PayPal Sandbox Setup Guide](https://developer.paypal.com/tools/sandbox/)

### Common WooCommerce + Elementor Issues and How to Fix Them

When integrating WooCommerce with Elementor, a few recurring issues tend to appear—especially around product templates, checkout pages, styles not applying, and conflicting plugins. Below is a concise troubleshooting section you can add to your blog post.

#### <ins>WooCommerce Pages Missing (Shop, Cart, Checkout, My Account)</ins>

| **Symptoms**               | **Fix**                                                         |
| -------------------------- | --------------------------------------------------------------- |
| Page not found errors      | Assign WooCommerce pages: **WooCommerce → Settings → Advanced** |
| Cart or Checkout blank     | Create missing pages and assign them                            |
| Shop redirects to homepage | Go to **Settings → Permalinks → Save** to flush permalinks      |


#### <ins>Elementor Template Not Applying to Product Pages</ins>

| **Symptoms**                                | **Fix**                                                         |
| ------------------------------------------- | --------------------------------------------------------------- |
| Custom single product template not showing  | Check **Theme Builder → Single Product → Display Conditions**   |
| Default theme template overrides Elementor  | Disable theme product layouts in **Customizer → WooCommerce**   |
| Only some products display the new template | Apply conditions to **All Products** instead of individual ones |

#### <ins>CSS or Styles Not Applying</ins>

| **Symptoms**                                   | **Fix**                                                 |
| ---------------------------------------------- | ------------------------------------------------------- |
| Colors, spacing, or fonts do not change        | Clear CSS cache: **Elementor → Tools → Regenerate CSS** |
| Styles overridden by theme or WooCommerce CSS  | Use more specific CSS selectors                         |
| Layout shifts when DOM Optimization is enabled | Disable **Optimized DOM Output** in Elementor Features  |
| Changes not showing after update               | Purge caching plugins + Cloudflare/LiteSpeed caches     |

#### <ins>Add to Cart Button Not Working (AJAX Issues)</ins>

| **Symptoms**                      | **Fix**                                                                    |
| --------------------------------- | -------------------------------------------------------------------------- |
| Clicking Add to Cart does nothing | Enable AJAX add-to-cart: **WooCommerce → Products → Add to Cart Behavior** |
| Cart does not refresh or update   | Disable JS optimization (Combine/Minify/Defer) in caching plugins          |
| Mini cart does not update         | Disable conflicting cart/mini-cart plugins temporarily                     |

#### <ins>Cart or Checkout Pages Breaking in Elementor</ins>

| **Symptoms**                             | **Fix**                                                                  |
| ---------------------------------------- | ------------------------------------------------------------------------ |
| Layout broken or fields misaligned       | Use Elementor’s **Cart** and **Checkout** widgets (Pro)                  |
| Buttons overlapping or sections missing  | Avoid editing native WooCommerce shortcodes                              |
| Shipping or payment sections not loading | Disable conflicting “One-Page Checkout” or checkout optimization plugins |

#### <ins>PayPal Payment Errors (Sandbox or Live)</ins>

| **Symptoms**                     | **Fix**                                                         |
| -------------------------------- | --------------------------------------------------------------- |
| Payment fails with error message | Ensure correct **Sandbox vs Live** API credentials              |
| Sandbox orders not completing    | Recreate sandbox accounts in developer dashboard                |
| PayPal button not showing        | Disable JS/cookie blockers or caching on checkout               |
| Hard-to-debug errors             | Enable logging → see logs under **WooCommerce → Status → Logs** |

#### <ins>Product Images Blurry or Wrong Size</ins>

| **Symptoms**                       | **Fix**                                        |
| ---------------------------------- | ---------------------------------------------- |
| Product images appear blurry       | Regenerate thumbnails via plugin               |
| Wrong cropping or dimensions       | Adjust WooCommerce image settings + regenerate |
| Images look stretched in Elementor | Set image widget to **Full** or correct ratio  |

#### <ins>Inventory Not Updating After Purchases</ins>

| **Symptoms**                                    | **Fix**                                              |
| ----------------------------------------------- | ---------------------------------------------------- |
| Stock level not decreasing                      | Check **Products → Inventory → Hold Stock** settings |
| Orders stuck in “Pending” causing stock to lock | Lower Hold Stock time or disable                     |
| Cached cart shows incorrect inventory           | Exclude Cart/Checkout from caching plugins           |

---

## Integrating Google Maps With Elementor

Elementor makes it simple to embed a Google Map, but adding **API keys**, **advanced map settings**, and **custom markers** requires a bit of setup.

### 1. Enable the Google Maps API & Get Your API Key

Before Elementor can render interactive Google Maps, you must enable the proper APIs inside the Google Cloud Console.

1. Visit **Google Cloud Console** → *APIs & Services*.
2. Enable at least:

   * **Maps JavaScript API**
   * **Geocoding API** (optional, for address lookups)
   * **Places API** (optional, for autocomplete)
     
3. Create or use an existing API key.
4. Restrict the key to your domain for security.

- [https://developers.google.com/maps/documentation/javascript](https://developers.google.com/maps/documentation/javascript)
- [https://console.cloud.google.com/apis](https://console.cloud.google.com/apis)

### 2. Adding a Google Map Using Elementor’s Built-In Widget

The **Elementor Google Maps widget** (free version) lets you quickly embed a basic map:

1. Drag **Google Maps** widget into your page.
2. In **Content → Location**, enter an address.
3. In **Settings**, adjust:

   * Zoom level
   * Height
   * Map Style (e.g., SnazzyMaps custom styles)

### Adding a Google Map With Custom Pins (Code Example)

To add a **custom pin icon**, you’ll load the Maps JavaScript API and initialize your own map inside an HTML widget.

**Steps**

1. Add an **HTML widget** inside Elementor.
2. Paste the following minimal code:

```html
<div id="customMap" style="width:100%;height:400px;"></div>

<script src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY"></script>
<script>
  function initMap() {
    const position = { lat: 40.741, lng: -73.989 };
    const map = new google.maps.Map(document.getElementById("customMap"), {
      center: position,
      zoom: 14,
      styles: [], // optional custom map styles
    });
    new google.maps.Marker({
      position,
      map,
      icon: {
        url: "https://yourdomain.com/path/custom-pin.png",
        scaledSize: new google.maps.Size(40, 40)
      }
    });
  }
  window.onload = initMap;
</script>
```

- [https://developers.google.com/maps/documentation/javascript/markers](https://developers.google.com/maps/documentation/javascript/markers)**

### Using Multiple Custom Pins (Dynamic or Static)

To add **multiple markers**, simply loop through a list:

```html
<script>
  const locations = [
    { lat: 40.741, lng: -73.989, icon: "/pins/blue.png" },
    { lat: 40.744, lng: -73.982, icon: "/pins/red.png" }
  ];
  function initMap() {
    const map = new google.maps.Map(document.getElementById("customMap"), {
      center: locations[0],
      zoom: 13
    });
    locations.forEach(loc => {
      new google.maps.Marker({
        position: loc,
        map,
        icon: {
          url: loc.icon,
          scaledSize: new google.maps.Size(36, 36)
        }
      });
    });
  }
  window.onload = initMap;
</script>
```

- [https://developers.google.com/maps/documentation/javascript/custom-markers](https://developers.google.com/maps/documentation/javascript/custom-markers)**

### Using Custom Map Styles (Dark Mode, Minimal, etc.)

You can apply custom map themes by using the **SnazzyMaps** plugin and pasting the style JSON into the map:

```js
const map = new google.maps.Map(document.getElementById("customMap"), {
  center: position,
  zoom: 14,
  styles: snazzyMapStyle
});
```

- [https://snazzymaps.com](https://snazzymaps.com)

### Making Map Widgets Reusable (Elementor Templates)

If you frequently embed maps with custom styling or icons:

1. Create a new **Elementor Template > Section**.
2. Insert your HTML-map widget.
3. Replace coordinates or icons with dynamic fields (ACF, Pods, or Elementor Custom Fields).
4. Save and reuse across pages.

This gives you consistent styling and faster site-building.

### Troubleshooting Common Google Maps Issues in Elementor

| Issue                                     | Fix                                                       |
| ----------------------------------------- | --------------------------------------------------------- |
| Map not loading                           | Verify API key, domain restrictions, billing enabled      |
| “For development purposes only” watermark | Enable billing in Google Cloud                            |
| Custom pin not appearing                  | Check URL path & icon size                                |
| Map crashes in Elementor preview          | Try viewing from front-end or disable conflicting plugins |

---

## Integrating Google Analytics With Elementor

Adding Google Analytics to your WordPress + Elementor site is essential for tracking pageviews, conversions, user behavior, and the performance of your Elementor layouts. Below are the most reliable methods, from using Elementor’s built-in tools (Pro) to adding the tracking code manually (Free).

### Why Track With Google Analytics?

* Understand which Elementor pages perform best
* Measure conversions for forms, buttons, popups, and funnels
* Improve UX using behavior insights and scroll-depth data
* Attribute traffic from marketing campaigns

### Using Elementor Pro (Recommended)

Elementor Pro provides a native **Site Settings → Integrations → Google Analytics** field.

**Steps**

1. In your Google Analytics dashboard (GA4), go to **Admin → Data Streams → Web → Measurement ID** (looks like `G-XXXXXXX`).
2. In WordPress, open:
   **Elementor → Settings → Integrations → Google Analytics**
3. Paste your Measurement ID.
4. Click **Save Changes**.
5. Clear cache.

Elementor automatically injects the GA4 tracking tag across your site—no manual code needed.

### Manual GA4 Code Injection (Elementor Free)

**Steps**

1. In GA4: **Admin → Data Stream → Add Tag → Global site tag (gtag.js)**.
2. Copy the script snippet.
3. Install a header/footer script plugin (e.g., WPCode Lite).
4. Add script to the header:

```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXX"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-XXXXXXX');
</script>
```
- [GA4 Setup Guide](https://support.google.com/analytics/answer/9304153)

### Tracking Elementor Events in GA4

Elementor widgets (forms, buttons, videos, popups) can be connected to Analytics events.

### Elementor Form Submissions → GA4 Event

Elementor Pro allows **Form → Actions After Submit → Webhook** or **Custom JS**.

Example custom JS event:

```js
document.addEventListener('elementorPro/forms/new', (event) => {
  gtag('event', 'form_submit', {
    form_name: event.detail.formName
  });
});
```

- [Elementor Form JS Docs](https://developers.elementor.com/docs/forms-api/)

### Tracking Scroll Depth (Elementor pages)

You can track scroll depth using GTM’s built-in triggers:

1. In GTM → **Triggers → Scroll Depth → Vertical 25/50/75/100**
2. Create GA4 “scroll” events.
3. Publish.

This works automatically across Elementor pages, including long-form landing pages.

### Tracking Elementor Ecommerce Conversions (WooCommerce + GA4)

Google Analytics 4 includes enhanced measurement for ecommerce, but WooCommerce + Elementor requires additional configuration so product views, add-to-cart events, and purchases are captured correctly.

Use the WooCommerce → Google Listings & Ads (Recommended, Free) plugin

**Steps**

1. Install **Google Listings & Ads** from Plugins → Add New.
2. Connect your Google account.
3. Enable **GA4 Ecommerce Tracking** in the setup wizard.
4. Verify events in **GA4 → Admin → DebugView**.

GA4 events handled automatically:

* `view_item`
* `add_to_cart`
* `begin_checkout`
* `purchase`
* `view_cart`

- [https://woocommerce.com/products/google-listings-and-ads/](https://woocommerce.com/products/google-listings-and-ads/)

### Tracking Button Clicks on Elementor Pages (GA4)

You can track clicks on any button inside Elementor—Pro or Free—using Google Tag Manager or custom JS.

### Tracking Video Plays on Elementor Pages (YouTube/Vimeo)

Elementor embeds videos using iframe players, so tracking requires GTM or the YouTube API.

**Steps**

1. In GTM → **Variables → Configure → Check "YouTube" variables**

   * Video Title
   * Video URL
   * Video Provider
   * Video Percent

2. Add a new **YouTube Video Trigger**

   * Trigger on: **Progress** (10%, 25%, 50%, 75%, 100%)
   * Enable: “Add JavaScript API support to all YouTube videos”

3. Create a **GA4 Event Tag**

   * Event Name: `video_progress`
   * Parameters: `video_title` → `{{Video Title}}`, `percent` → `{{Video Percent}}`

Works even for videos placed inside Elementor widgets, popups, tabs, or sliders.

---

## Integrating Typeform with Elementor

Embedding a Typeform inside Elementor is one of the quickest ways to add high-conversion forms, quizzes, surveys, or lead-gen flows to your WordPress pages. Typeform handles the form logic and design, while Elementor gives you full control over layout and styling around it.

### Generate Your Typeform Embed Code

1. Log into **Typeform** → open your form.
2. Go to **Share → Embed in a Web Page**.
3. Choose your preferred embed style:

   * **Standard** (inline iframe)
   * **Popup** (button or link trigger)
   * **Slider**
   * **Popover**
    
4. Click **Get the code** and copy the HTML/JavaScript snippet.

- [https://www.typeform.com/help/a/embed-your-typeform-360029581131/](https://www.typeform.com/help/a/embed-your-typeform-360029581131/)

### Add the Typeform to Elementor (Inline Embed)

If you want the form to appear directly on the page:

1. Edit your page with **Elementor**.
2. Drag in an **HTML widget**.
3. Paste the Typeform embed snippet.

```html
<div style="width:100%;height:500px;">
  <iframe
    src="https://form.typeform.com/to/abcd1234"
    style="width:100%;height:100%;border:none;"
    allow="camera; microphone; autoplay; encrypted-media;"
  ></iframe>
</div>
```

- [https://developers.typeform.com/embed/](https://developers.typeform.com/embed/)

### Add a Popup Typeform (Button or Link Trigger)

Popup embeds are great for keeping pages clean while still capturing leads.

1. In Typeform → **Share → Popup** → choose Button or Link.
2. Copy the embed JS snippet.
3. In Elementor:

   * Add an **HTML widget** at the bottom of the page or in a global footer.
   * Paste the entire embed script.
     
4. Add a regular **Button widget**.
5. Set the button’s **Link** to the Typeform's trigger class (usually something like `.typeform-share`).


```html
<a class="typeform-share" href="https://form.typeform.com/to/abcd1234" data-mode="popup">
  Open Survey
</a>
<script>
  (function() {
    var d = document,
    gi = d.getElementById,
    ce = d.createElement,
    gt = d.getElementsByTagName,
    id = "typef_orm",
    b = "https://embed.typeform.com/";
    if (!gi.call(d, id)) {
      var js = ce.call(d, "script");
      js.id = id;
      js.src = b + "embed.js";
      var q = gt.call(d, "script")[0];
      q.parentNode.insertBefore(js, q);
    }
  })();
</script>
```

- [https://developer.typeform.com/embed/modes/#popup](https://developer.typeform.com/embed/modes/#popup)

### Adjusting Width, Height & Responsiveness

Typeform’s iframe is fully responsive, but you may want customized sizing depending on your layout.
To make the embed full-height inside a section:

1. Set the **Column** or **Section** height to *Min Height* in Elementor.
2. Set **min-height: 100vh** or any custom height.
3. Ensure your iframe includes `height:100%`.

### Styling Surrounding Elements in Elementor

Typeform’s embed itself can’t be styled directly from Elementor, but everything around it can:

* Add padding/margins around the HTML widget
* Wrap the form in a **Container** with background colors/images
* Add headings, icons, progress bars, CTAs
* Add animations (scroll, fade-in) to the section or container

If you need more visual control, use the **Standard embed** (iframe) and give it a wrapper div to style.

### Tracking Typeform Conversions with GA4 or GTM

Typeform supports event callbacks (via Embed SDK) and also sends built-in completion events.

**Quick tracking method using GTM:**

```javascript
window.addEventListener("message", function(event) {
  if (event.data.type === "form-submit") {
    dataLayer.push({ event: "typeform_submission" });
  }
});
```

Add this inside the same HTML widget that loads the Typeform.

- [https://developer.typeform.com/embed/usage/#event-tracking](https://developer.typeform.com/embed/usage/#event-tracking)

### Troubleshooting

**Form not loading?**

* Make sure no caching plugin is delaying or stripping Typeform scripts.
* Disable “Optimize JS” or defer settings temporarily.

**Popup not opening?**

* You must include the Typeform embed JS code somewhere on the page.
* If using multiple popups, ensure each trigger has the correct `data-mode`.

---

# Conclusion

Mastering Elementor is fundamentally about mastering process not just design. With a fast, automated dev environment powered by Laravel Valet, WP-CLI, and modern theme frameworks like Astra, you can build, test, rollback, version, and customize Elementor projects with speed and confidence.
