# Mastering Elementor

**Time to Read:** ~13 minutes

Elementor has evolved into one of the most powerful visual builders in the WordPress ecosystem. 
This guide delivers a clear, technical path to mastering Elementor.

---

### Local Setup with Valet, WP-CLI & Astra/Elementor

#### 1. Install Prereqs (macOS)

```bash
# Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# PHP, MySQL, Mailpit, WP-CLI, Composer
brew install php mysql mailpit wp-cli composer
brew services start mysql
```

Homebrew: [https://brew.sh](https://brew.sh)
PHP: [https://formulae.brew.sh/formula/php](https://formulae.brew.sh/formula/php)
MySQL: [https://formulae.brew.sh/formula/mysql](https://formulae.brew.sh/formula/mysql)
Mailpit: [https://github.com/axllent/mailpit](https://github.com/axllent/mailpit)
WP-CLI: [https://wp-cli.org](https://wp-cli.org)
Composer: [https://getcomposer.org](https://getcomposer.org)

---

#### 2. Install & Configure Laravel Valet

```bash
composer global require laravel/valet
export PATH="$HOME/.config/composer/vendor/bin:$PATH"  # or ~/.composer/vendor/bin
valet install

mkdir -p ~/Sites && cd ~/Sites
valet park
```

Laravel Valet: [https://laravel.com/docs/valet](https://laravel.com/docs/valet)

---

#### 3. Create a New WordPress Site

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

WordPress: [https://wordpress.org/download](https://wordpress.org/download)
Valet Link: [https://laravel.com/docs/valet#the-link-command](https://laravel.com/docs/valet#the-link-command)
WP-CLI Core: [https://developer.wordpress.org/cli/commands/core](https://developer.wordpress.org/cli/commands/core)

---

#### 4. Create / Reset the Database & Site

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

WP-CLI DB: [https://developer.wordpress.org/cli/commands/db](https://developer.wordpress.org/cli/commands/db)
WP-CLI Site Empty: [https://developer.wordpress.org/cli/commands/site/empty](https://developer.wordpress.org/cli/commands/site/empty)

---

#### 5. Install Astra & Elementor

```bash
wp theme install astra --activate
wp plugin install elementor --activate
# wp plugin install /path/to/elementor-pro.zip --activate
```

Astra Theme: [https://wpastra.com](https://wpastra.com)
Elementor: [https://elementor.com](https://elementor.com)
WP-CLI Theme: [https://developer.wordpress.org/cli/commands/theme](https://developer.wordpress.org/cli/commands/theme)
WP-CLI Plugin: [https://developer.wordpress.org/cli/commands/plugin](https://developer.wordpress.org/cli/commands/plugin)

---

#### 6. Mailpit for Email Testing

```bash
mailpit
```

Mailpit Docs: [https://github.com/axllent/mailpit](https://github.com/axllent/mailpit)

SMTP: `127.0.0.1:1025`
UI: `http://localhost:8025`

---

# 2. Free vs Pro: What You Should Actually Use

Both versions of Elementor are strong, but the **Pro** version unlocks workflow efficiencies that matter for production environments.

| Feature                                      | Free    | Pro  |
| -------------------------------------------- | ------- | ---- |
| Drag-and-drop page builder                   | Yes     | Yes  |
| Theme Builder (Header, Footer, Archive, 404) | No      | Yes  |
| Dynamic Fields / ACF / CPT Support           | No      | Yes  |
| Popup Builder                                | No      | Yes  |
| WooCommerce Builder                          | Limited | Full |
| Advanced widgets (Forms, Posts, Nav Menu)    | No      | Yes  |
| Custom CSS per element                       | Basic   | Full |
| Motion effects, scroll effects               | Basic   | Full |

Recommendation:
If you're building more than two commercial sites per year or using CPT/ACF, Elementor Pro pays for itself immediately.

---

# 3. Rolling Back Elementor Versions

Elementor provides version control inside WordPress. This is invaluable when troubleshooting plugin conflicts or regressions.

### Roll back from Dashboard

WordPress Admin →
**Elementor → Tools → Version Control → Rollback**

### Using WP-CLI

Run:

```bash
wp plugin install elementor --version=3.20.1 --force
```

Replace with required version number.

---

# 4. Keyboard Shortcuts for Power Users

| Action                   | Shortcut             |
| ------------------------ | -------------------- |
| Show Navigator           | Cmd/Ctrl + I         |
| Finder (search elements) | Cmd/Ctrl + E         |
| Switch Panel ↔ Canvas    | Cmd/Ctrl + P         |
| Undo                     | Cmd/Ctrl + Z         |
| Redo                     | Cmd/Ctrl + Shift + Z |
| Save                     | Cmd/Ctrl + S         |
| Responsive Mode          | Cmd/Ctrl + Shift + M |

Full list:
[https://elementor.com/help/keyboard-shortcuts](https://elementor.com/help/keyboard-shortcuts)

---

# 5. Adding and Managing Favorite Widgets

Elementor allows pinning frequently used widgets to speed up workflow.

Steps:

1. Open Elementor editor
2. Hover any widget → Right-click
3. Choose **Add to Favorites**

This creates a “Favorites” tab for fast access.

---

# 6. Setting Global Typography and Styles

Consistency is critical when working at scale.

### Where to Configure

WordPress Admin →
**Elementor → Site Settings**

Configure:

* Global colors
* Global typography
* Buttons
* Form fields
* Images
* Theme styles

Once saved, all new widgets inherit defaults unless manually overridden.

---

# 7. Setting Headers and Footers (Theme Builder)

Requires Elementor Pro.

### Create a Global Header

1. Templates → Theme Builder → Header
2. Add new template
3. Use Nav Menu + Logo widget
4. Publish with conditions:

   * **Entire Site**, or
   * Specific post types, categories, or pages

### Create a Global Footer

Same process via Theme Builder → Footer.

---

# 8. Using Templates and Blocks (Import/Export Included)

### Insert Library Templates

Inside Elementor editor:

* Template → Add Template
* Choose from **Blocks**, **Pages**, or **My Templates**

### Export Your Template

Templates → Saved Templates → Export JSON

### Import Template

Templates → Import Templates → Upload JSON

Great for sharing components across client projects or maintaining your own starter kits.

---

# 9. Using Custom CSS and JavaScript

### Elementor Pro

Per-widget CSS is available under:
Advanced → Custom CSS

### Site-wide CSS/JS

Use:

```php
function me_enqueue_scripts() {
    wp_enqueue_style('me-custom', get_stylesheet_directory_uri() . '/custom.css');
    wp_enqueue_script('me-custom-js', get_stylesheet_directory_uri() . '/custom.js', [], null, true);
}
add_action('wp_enqueue_scripts', 'me_enqueue_scripts');
```

Place inside `functions.php` of your child theme.

---

# 10. Text Animations (Typing Effects, Transitions, Scroll Animations)

Elementor Pro includes motion effects:

* Entrance animations
* Scrolling effects (parallax, rotate, opacity)
* Mouse-track animations
* Transformations (scale, rotate, skew)

For typing animations, use:

* Elementor’s built-in "Animated Headline" widget, or
* Custom JS such as Typed.js when finer control is needed.

Example:

```javascript
var typed = new Typed('.typed-text', {
  strings: ["Mastering Elementor", "Building Modern Websites"],
  typeSpeed: 50,
  backSpeed: 25,
  loop: true
});
```

# 11. Integrating Elementor with ACF (Advanced Custom Fields)

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
