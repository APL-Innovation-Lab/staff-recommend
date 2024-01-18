
# Drupal Faceted Browsing Setup Guide

This guide provides instructions on setting up a Drupal site with a "Staff Recommend" content type, faceted browsing using two vocabularies (Audience and Recommend Tags), and configuring various site settings.

## Prerequisites
- A fresh Drupal installation.
- Basic knowledge of Drupal administration.

## Step 1: Install Necessary Modules

Install the following modules:
- Search API
- Facets

You can install these modules via the Drupal UI or using Drush:
```bash
drush en search_api facets restui -y
```

## Step 2: Create Vocabularies

1. Navigate to `Structure -> Taxonomy -> Add vocabulary`.
2. Create two vocabularies: "Audience" and "Recommend Tags".

## Step 3: Create Content Type

1. Navigate to `Structure -> Content types -> Add content type`.
2. Create a content type named "Staff Recommend".
3. Add fields as required, including entity reference fields for the "Audience" and "Recommend Tags" vocabularies.

## Step 4: Import Taxonomy Terms

To import taxonomy terms:
1. Navigate to `Structure -> Taxonomy` and select the relevant vocabulary (e.g., Audience).
2. Click on `Add term`.
3. Enter the details for the term and save.

Repeat the process for each term you want to add to the vocabularies.

Example terms:
- For "Audience": Adults, Teens, Children
- For "Recommend Tags": Must Read, Staff Pick


## Step 5: Adjust Permitted HTML Tags to Include `iframe`

To include `iframe` tags in Views, you'll need to modify the `Xss.php` file in the Drupal core. This is not a typical practice and is generally discouraged. Proceed with caution and consider the potential risks.

1. **Locate the `Xss.php` File**:
   - Find the `Xss.php` file in your Drupal installation. It's typically located in `core/lib/Drupal/Component/Utility`.

2. **Modify the `Xss.php` File**:
   - Open `Xss.php` in a text editor.
   - Find the array of allowed HTML tags. This is usually a static function named `getHtmlTagList()`.
   - Add `'iframe'` to this array.
   - Save your changes.

   Example:
   ```php
   protected static function getHtmlTagList() {
     return [
       // Existing tags...
       'iframe' => [],
       // ...other tags
     ];
   }
   ```

3. **Clear Drupal's Cache**:
   - After making changes, clear Drupal's cache to ensure your changes take effect.

### Important Considerations:
- **Backup**: Always backup the file and your database before making any changes.
- **Updates**: Remember that updating Drupal core will overwrite your changes. You'll need to reapply them after each update.
- **Security**: Allowing additional tags, especially `iframe`, can increase security risks. Ensure that only trusted users have the ability to use these tags.
- **Alternative Solutions**: Consider using modules that allow iframe embeds securely, such as the 'Media' or 'Entity Embed' modules, as a safer alternative to editing core files.


## Step 6: Configure Path Settings

For path alias patterns:
1. Navigate to `Configuration -> Search and metadata -> URL aliases -> Patterns`.
2. Configure patterns for content and taxonomy terms as desired.

Example pattern for "Staff Recommend" nodes: `/staff-recommend/[node:title]`

## Step 7: Set Up Search Index

1. Navigate to `Configuration -> Search and metadata -> Search API`.
2. Add a new index for the "Staff Recommend" content type.
3. Add necessary fields to the index, including reference fields for "Audience" and "Recommend Tags".

## Step 8: Configure Facets

1. Navigate to `Configuration -> Search and metadata -> Facets`.
2. Create new facets for "Audience" and "Recommend Tags".
3. Configure facet display settings.

## Step 9: Create a View for Faceted Browsing

1. Navigate to `Structure -> Views -> Add view`.
2. Create a view that shows "Staff Recommend" content.
3. Integrate facets with the view.

## Step 10: Place Facet Blocks

Using either the Block layout or Layout Builder:
1. Place your facet blocks in the desired regions on your site.

## Testing the Setup

After setting up, create at least two "Staff Recommend" items and assign different terms from your vocabularies. Example entries:
- **Item 1**: Title: "Summer Reads", Audience: Adults, Tags: Must Read
- **Item 2**: Title: "Youth Adventure", Audience: Teens, Tags: Staff Pick

Index these items and test the facets on the created view page.

## Final Steps

- Re-index your content after making changes to the fields or configurations.
- Test the setup thoroughly.
- Adjust configurations based on test results.

## Additional Notes

This guide assumes familiarity with Drupal's administrative interface and basic site-building concepts. Adjust steps as necessary to fit your specific Drupal version or requirements.
