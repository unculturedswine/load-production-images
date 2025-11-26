# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a WordPress plugin called "Load Production Images" that redirects media requests from local/staging environments to a production server. This solves the common development problem of needing production images without downloading gigabytes of files.

## Architecture

### Core Components

1. **Main Plugin File** (`load-production-images.php`): Single-file plugin containing all functionality
   - `Load_Production_Images` class using singleton pattern
   - Settings page with WordPress Settings API
   - Multiple WordPress filters for URL rewriting
   - JavaScript fallback for failed image loads

### Key Features

- Redirects all upload URLs to production server
- Automatic detection prevents running on production (avoids infinite loops)
- WordPress Multisite support with configurable site ID
- Optional JavaScript fallback for images not found on production
- Toggle to enable/disable without deactivating plugin
- Admin notices showing current status

## Development Commands

Since this is a WordPress plugin without build tools:

```bash
# No build/compile steps required - this is a traditional WordPress plugin

# To test the plugin:
# 1. Copy the plugin folder to wp-content/plugins/
# 2. Activate via WordPress admin dashboard
# 3. Configure production URL in Settings > Load Production Images

# Check PHP syntax (if PHP CLI is available):
php -l load-production-images.php
```

## WordPress Coding Standards

Follow WordPress PHP coding standards when making modifications:
- Use tabs for indentation
- Use WordPress Settings API for options
- Escape output with appropriate functions (`esc_url()`, `esc_attr()`, `esc_html()`)
- Use `wp_json_encode()` for JavaScript data

## WordPress Filters Used

The plugin hooks into these filters to rewrite URLs:
- `upload_dir` - Modifies the base upload directory URL
- `wp_get_attachment_url` - Rewrites individual attachment URLs
- `wp_calculate_image_srcset` - Rewrites responsive image srcset URLs
- `the_content` - Replaces URLs in post content
- `post_thumbnail_html` - Replaces URLs in thumbnails
- `get_avatar` - Replaces URLs in avatars
- `widget_text` - Replaces URLs in text widgets
- `wp_get_attachment_image` - Replaces URLs in attachment images
- `wp_get_attachment_image_src` - Replaces URLs in image src arrays

## Options Storage

All settings stored in single option `lpi_options`:
- `enabled` - Boolean, whether plugin is active
- `live_site_url` - String, production server URL
- `is_multisite` - Boolean, whether production is multisite
- `multisite_id` - Integer, site ID for multisite installations
- `enable_local_fallback` - Boolean, whether to fall back to local images

## Security Considerations

- Production detection prevents activation on live site
- Settings require `manage_options` capability
- URLs are sanitized with `esc_url_raw()`
- JavaScript uses `wp_json_encode()` for safe data passing

## JavaScript Fallback

When enabled, the plugin outputs a footer script that:
- Listens for image error events
- Attempts to load from local uploads if production 404s
- Uses MutationObserver to handle dynamically added images
- Tracks attempted fallbacks to prevent infinite loops
