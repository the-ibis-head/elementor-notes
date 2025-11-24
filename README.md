# Mastering Elementor

**Estimated Reading Time:** ~18–22 minutes

Elementor has evolved into a full-stack site-building ecosystem. To build high-quality, scalable environments, developers must be able to work locally, extend templates, customize WooCommerce, implement advanced animations, and integrate APIs.

This guide provides a detailed, developer-focused walkthrough across every major Elementor capability.

---

## Local Development Setup with Laravel Valet and WP-CLI

### Install Valet

```bash
composer global require laravel/valet
valet install
```

### Setup WordPress

```bash
mkdir ~/Sites/my-elementor-site
cd ~/Sites/my-elementor-site

wp core download
wp config create --dbname=elementor --dbuser=root
wp db create

wp core install \
  --url="my-elementor-site.test" \
  --title="Elementor Lab" \
  --admin_user="admin" \
  --admin_password="password" \
  --admin_email="you@example.com"
```

Park the directory:

```bash
valet park
```

**References:**

* [https://laravel.com/docs/valet](https://laravel.com/docs/valet)
* [https://wp-cli.org/](https://wp-cli.org/)

---

## Elementor Free vs. Elementor Pro

### Free features

* Core widget library
* Drag-and-drop builder
* Basic templates
* Basic responsive settings

### Pro features

* Theme Builder (headers, footers, archives, single templates)
* WooCommerce Builder
* Popup Builder
* Advanced form widgets
* Dynamic data
* Lottie, flip boxes, posts, global widgets

**Reference:** [https://elementor.com/pricing/](https://elementor.com/pricing/)

---

## Rolling Back to Previous Versions

### WordPress Repository (Elementor Free)

Download older versions:
[https://wordpress.org/plugins/elementor/advanced/](https://wordpress.org/plugins/elementor/advanced/)

### WP-CLI Rollback

```bash
wp plugin install elementor --version=3.22.0 --force
wp plugin install elementor-pro --version=3.22.1 --force
```

---

## Keyboard Shortcuts

| Shortcut             | Action               |
| -------------------- | -------------------- |
| Ctrl/Cmd + Shift + L | Navigator            |
| Ctrl/Cmd + E         | Finder               |
| Ctrl/Cmd + P         | Command Search       |
| Ctrl/Cmd + S         | Save                 |
| Ctrl/Cmd + I         | Inline Editing Panel |

**Reference:** [https://elementor.com/help/keyboard-shortcuts/](https://elementor.com/help/keyboard-shortcuts/)

---

## Adding Favorite Widgets

1. Right-click a widget in the panel.
2. Click “Add to Favorites.”
3. Access under the **Favorites** tab.

---

## Setting Global Typography and Styles

Navigate to:
Elementor → Site Settings → Global Styles → Typography

Configure:

* Body text
* Heading hierarchy
* Link styles
* Global color palette

**Reference:** [https://elementor.com/help/global-settings/](https://elementor.com/help/global-settings/)

---

## Creating Headers and Footers Using Theme Builder

Steps:

1. Go to Templates → Theme Builder
2. Select **Header** or **Footer**
3. Build the layout
4. Set Display Conditions (Entire Site, Single Page, Archive, WooCommerce, etc.)

---

## Using Templates and Blocks (Including Export/Import)

### Export Template

Templates → Saved Templates → Export

### Import Template

Templates → Import Templates → Upload JSON

### Render Template Programmatically

```php
echo \Elementor\Plugin::$instance
  ->frontend
  ->get_builder_content_for_display(123);
```

**Reference:** [https://elementor.com/help/templates/](https://elementor.com/help/templates/)

---

## Using Custom CSS and JavaScript

### Elementor Pro Custom CSS

```css
selector:hover {
  transform: scale(1.05);
}
```

### Theme-Level JavaScript

`/wp-content/themes/your-theme/js/custom.js`

```javascript
document.addEventListener('DOMContentLoaded', () => {
  console.log("Custom Elementor script loaded.");
});
```

Enqueue the script:

```php
add_action('wp_enqueue_scripts', function () {
    wp_enqueue_script(
        'custom-js',
        get_stylesheet_directory_uri().'/js/custom.js',
        [],
        false,
        true
    );
});
```

---

## Using Text Animations

Example using Typed.js:

```html
<span id="typed"></span>

<script>
new Typed('#typed', {
  strings: ["Fast.", "Flexible.", "Powerful."],
  typeSpeed: 50,
  loop: true
});
</script>
```

---

## GSAP Animations and Video-Scrolling

### Basic GSAP Animation

```javascript
gsap.from(".hero-title", {
  y: 80,
  opacity: 0,
  duration: 1.2
});
```

### GSAP ScrollTrigger with Video Sync

```javascript
gsap.registerPlugin(ScrollTrigger);

ScrollTrigger.create({
  trigger: ".video-section",
  start: "top top",
  end: "bottom bottom",
  scrub: true,
  onUpdate: (self) => {
    const video = document.querySelector("video");
    video.currentTime = video.duration * self.progress;
  }
});
```

**Reference:** [https://gsap.com/](https://gsap.com/)

---

## Integrating Google Analytics

### Recommended: Site Kit by Google

[https://wordpress.org/plugins/google-site-kit/](https://wordpress.org/plugins/google-site-kit/)

### Manual GA4 Installation

```php
add_action('wp_head', function () {
?>
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXX"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-XXXX');
</script>
<?php
});
```

---

## Integrating Google Maps

### Elementor Pro Map Widget

Requires API key:
[https://developers.google.com/maps/documentation/javascript/get-api-key](https://developers.google.com/maps/documentation/javascript/get-api-key)

### Basic Embed

```html
<iframe 
 height="400"
 width="100%"
 src="https://www.google.com/maps/embed/v1/place?key=YOUR_KEY&q=Boston,MA">
</iframe>
```

---

## Integrating Typeform

Embed via HTML widget:

```html
<div data-tf-live="xxxxxx"></div>
<script src="//embed.typeform.com/next/embed.js"></script>
```

---

## Integrating and Customizing WooCommerce with PayPal Payments

Install plugin:
[https://wordpress.org/plugins/woocommerce-paypal-payments/](https://wordpress.org/plugins/woocommerce-paypal-payments/)

Configure in:

WooCommerce → Settings → Payments → PayPal

Supports:

* Smart Buttons
* Pay Later
* Vaulting
* Subscriptions (with add-ons)

---

## Customizing WooCommerce Product Pages

### Adjust Quantity Input Minimum

```php
add_filter('woocommerce_quantity_input_args', function ($args) {
    $args['min_value'] = 2;
    return $args;
});
```

### Remove Tabs

```php
add_filter('woocommerce_product_tabs', function ($tabs) {
    unset($tabs['reviews']);
    return $tabs;
});
```

---

## Using WC CLI Commands

```bash
wp wc product list
wp wc order list --status=completed
wp wc customer create --email="test@example.com"
```

**Reference:** [https://woocommerce.com/document/cli/](https://woocommerce.com/document/cli/)

---

## Using the WooCommerce REST API

### List Products

```bash
curl https://example.com/wp-json/wc/v3/products \
  -u consumer_key:consumer_secret
```

### Create Product

```bash
curl -X POST https://example.com/wp-json/wc/v3/products \
  -u ck:cs \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Custom Elementor Product",
    "type": "simple",
    "regular_price": "29.99"
  }'
```

**API Reference:**
[https://woocommerce.github.io/woocommerce-rest-api-docs/](https://woocommerce.github.io/woocommerce-rest-api-docs/)

---

## Creating Custom Plugins That Integrate with Elementor

### Basic Plugin Loader

`wp-content/plugins/elementor-lab/elementor-lab.php`

```php
<?php
/**
 * Plugin Name: Elementor Lab
 */

add_action('elementor/widgets/widgets_registered', function () {
    require_once __DIR__.'/widgets/my-widget.php';
});
```

### Example Custom Elementor Widget

```php
class My_Custom_Widget extends \Elementor\Widget_Base {

    public function get_name() { return 'my_widget'; }
    public function get_title() { return 'My Widget'; }
    public function get_icon() { return 'eicon-code'; }

    protected function render() {
        echo "<div class='my-widget'>Hello from a custom widget.</div>";
    }
}
```

---

## Final Thoughts

Elementor is far more powerful than a traditional visual builder. When combined with modern local development workflows, dynamic data, GSAP animations, REST APIs, Typeform integrations, and WooCommerce customization, it becomes a full web application layer on top of WordPress.
