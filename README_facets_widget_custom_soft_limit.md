
# Patching Facets Widget for Custom Soft Limit

## Situation
We identified a need to offer a custom soft limit option (`14`) for a Facets widget in Drupal, which wasn't available by default in the Facets module's configuration options. The Facets module is a contributed module used for creating faceted search interfaces.

## Achieving the Customization
To include `14` as an option for the soft limit, we altered the `buildConfigurationForm` method within the Facets widget plugin code. Specifically, we added `14` to the `$options` array that defines the available choices for the soft limit in the widget's configuration form.

## Code Alteration
The alteration was made in the widget plugin's PHP file, typically located in the module's `Plugin/facets/widget` directory. We modified the `$options` array within the `buildConfigurationForm()` method to include `14` as shown below:

```php
$options = [50, 40, 30, 20, 15, 14, 10, 5, 3];
```

## Maintaining Customization Across Updates
When the contributed module (Facets in this case) receives updates, customizations like this can be overwritten. To preserve the customization, we use a patching workflow. Here's how to create and apply patches for this customization:

### Step 1: Create a Patch
1. After making your changes, navigate to your Drupal project's root directory in the terminal.
2. Use the `git diff` command to generate a patch file for your changes. If your changes are in the `facets` module, the command might look like this:
   ```bash
   git diff modules/contrib/facets > patches/custom_soft_limit.patch
   ```
3. This command creates a patch file (`custom_soft_limit.patch`) containing the differences.

### Step 2: Apply the Patch
Whenever the Facets module is updated, you'll need to re-apply your patch to maintain the customization.

1. Store your patch file in a dedicated directory within your project, such as `patches/`.
2. Modify your project's `composer.json` to apply the patch automatically when installing or updating the Facets module. Add the following lines to the `extra` section:
   ```json
   "patches": {
     "drupal/facets": {
       "Custom soft limit option": "patches/custom_soft_limit.patch"
     }
   }
   ```
3. Use Composer to apply the patch. Running `composer install` or `composer update` will now also apply your custom patch.

### Additional Notes
- Ensure you have the `cweagans/composer-patches` plugin installed in your project to apply patches via Composer.
- Test the patch application in a development environment before deploying it to production.

## Conclusion
By following this workflow, you can ensure that your customizations to the Facets module are maintained across module updates, keeping the `14` option available for the soft limit in your Facets widgets.
