# Site Index

Load images from your production server on local development or staging environments without downloading gigabytes of images. Supports multisite installations and includes automatic fallback to local images when production returns 404.

---

=== Load Production Images ===
Contributors: Kinda Useful Plugins
Tags: development, staging, images, media, localhost
Requires at least: 5.0
Tested up to: 6.7
Stable tag: 1.0.2
Requires PHP: 7.0
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html

Load images from your production server on local or staging environments.

== Description ==

Load Production Images solves the common development problem of needing production media files on local or staging environments. Instead of downloading gigabytes of images, this plugin redirects media requests to your production server.

Features:

* Load images from production on local/staging environments
* Automatic detection prevents activation on production
* WordPress Multisite support with site ID configuration
* Optional fallback to local images when production returns 404
* Lightweight with no performance impact on production
* Simple toggle to enable/disable without deactivating

== Installation ==

1. Upload the plugin folder to the `/wp-content/plugins/` directory
2. Activate the plugin through the 'Plugins' menu in WordPress
3. Navigate to Settings > Load Production Images
4. Enter your production server URL
5. Enable image loading

== Frequently Asked Questions ==

= Will this work on my production server? =

No, and that's intentional. The plugin automatically disables itself when it detects you're on the production server to prevent infinite loops.

= Does this support WordPress Multisite? =

Yes, check the multisite option and enter the site ID to load from the correct uploads/sites/X/ directory.

= What if some images exist locally? =

Enable the "Local Fallback" option to automatically use local images when production returns 404.

== Changelog ==

= 1.0.2 =
* Fixed checkbox settings not saving correctly when unchecked

= 1.0.1 =
* Fixed admin notice persistence - dismissing the notice now saves to user preferences
* Notice reappears when plugin settings are changed to confirm new configuration

= 1.0.0 =
* Initial release

== License ==

This plugin is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 2 of the License, or (at your option) any later version.

This plugin is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.
