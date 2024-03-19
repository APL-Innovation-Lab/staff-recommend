# Staff Recommend Page Adjustment Guide

This document outlines the process for adjusting the **Staff Recommend** page on the Austin Public Library website using the Drupal Content Management System (CMS). It covers the creation of a new page, layout customization, and the configuration of Facets blocks and views to enhance content discovery and presentation.

## Creating the Staff Recommend Page

1. **Page Creation:**
   - Navigate to the Drupal UI to create a new Page node at `/node/add/page_`.
   - Fill in the necessary details:
     - Title: `Staff Recommend`
     - URL Alias: `/staff-recommend`
     - Main Image and Introduction Text as per your content strategy.
   - The default visibility settings for the content are kept as is.

2. **Layout Customization:**
   - After the Page node is created, customize the layout by accessing `/node/[the-new-node-id]/layout`.
   - Ensure the layout changes affect **only this node** and not all content of the Page type.
   - Add **Facets blocks** and **Facets view** to the layout as required for content presentation.

3. **Facets View Adjustment:**
   - The Facets view is crucial for sorting and displaying content based on recent updates.
   - Access the Facets view settings at `/admin/structure/views/view/staff_recommend_facets`.
   - Adjust the **Sort criteria** from "random" to "changed" to ensure the most recently updated lists are shown first.

4. **Adding Accordion Content:**
   - Attach nodes of the Accordion content type to the page for additional resources or information. Example nodes included:
     - Book Recommendation Resources (Node ID: 1734652)
     - Books in World Languages (Node ID: 1734653)

## Additional Notes

- For detailed information on creating and configuring Facets blocks, refer to the documentation available at the root of this repository.
- It's imperative to test the changes in a development environment or with a preview option before finalizing the adjustments to ensure they meet the intended design and functionality requirements.

## Conclusion

By following these steps, site administrators and content editors can effectively customize the **Staff Recommend** page to enhance user engagement and content discoverability. This guide ensures a consistent approach to page adjustments while maintaining the flexibility to incorporate specific content needs.