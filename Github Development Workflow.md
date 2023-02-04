---
title: Github Development Workflow
created: '2022-03-14T13:27:51.274Z'
modified: '2022-03-14T14:57:42.889Z'
---

# Github Development Workflow

## Understood Github workflow

This is the intended workflow which should have been followed as per my understanding.

Create a branch `develop` from `main`.

### Basic Plugin Tasks

#1 **Register Custom Post Types and Taxonomies**

Create a branch `feat/cpt` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review.

#2 **Register Custom Meta Box Movie Post Type Metadata**

Create a branch `feat/movie-metadata` from `feat/cpt`. Work on this feature. Raise a PR against `feat/cpt` for peer code review. 

#3 **Register Custom Meta Box Person Post Type Metadata**

Create a branch `feat/person-metadata` from `feat/cpt`. Work on this feature. Raise a PR against `feat/cpt` for peer code review.

These three tasks have dependencies as they need custom post type and taxonomies. So, once this gets completed and all three PRs are merged to `feat/cpt`. Merge `feat/cpt` to `develop`.

#18 **Register Custom Meta Box for Photo and Video Gallery**

Create a branch `feat/gallery-metabox` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. On approval, merge it to `develop`.

#4 **Register Shortcodes**

Create a branch `feat/shortcodes` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. On approval, merge it to `develop`.

#5 **Register Settings Page**

Create a branch `feat/plugin-settings` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. On approval, merge it to `develop`.

Here, basic plugin assignment is completed and `develop` branch has the basic plugin assignment tasks. So, create a branch `feat/plugin` from develop and raise a PR from `feat/plugin` against `main` for code review by Chandra. Address feedbacks in this PR and branch `feat/plugin`.

### Basic theme tasks

#14 **Create Child theme**

Create a branch `feat/child-theme` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. Get its approval before moving to next task. Merge it to `develop`.

#9 **Single Page Template - Movie**

Create a branch `feat/single-page-movie` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. On approval, merge it to `develop`.

#10 **Archive Page Template - Movie**

Create a branch `feat/archive-page-movie` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. On approval, merge it to `develop`.

#11 **Single Page Template - Person**

Create a branch `feat/single-page-person` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. On approval, merge it to `develop`.

#12 **Archive Page Template - Person**

Create a branch `feat/archive-page-person` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. On approval, merge it to `develop`.

Here, basic theme assignment is completed and `develop` branch has the basic theme assignment features. Create a branch `feat/theme` from develop. Till here, `feat/plugin` should have been merged to `main`. Raise a PR from `feat/theme` against `main` for code review by Chandra & Paul. Address feedbacks in this PR, branch `feat/theme` and on approval, merge it to `main`.

### Advance Plugin Tasks

Tasks in this module don't have any dependencies.So, for every task, branch is created from `develop`.

#6 **Add Dashboard Widgets**

Create a branch `feat/dashboard-widgets` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. After peer approval, add Chandra and Paul as reviewers.

#16 **Create custom user role**

Create a branch `feat/custom-user-role` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. After peer approval, add Chandra and Paul as reviewers.

#17 **Add rewrite rules/permalink structure for custom post types**

Create a branch `feat/custom-rewrite-rules` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. After peer approval, add Chandra and Paul as reviewers.

#19 **Create custom database tables**

Create a branch `feat/custom-db-tables` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. After peer approval, add Chandra and Paul as reviewers.

### REST API

#22 **Create custom REST API endpoints**

Create a branch `feat/custom-rest-endpoints` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. After peer approval, add Chandra and Paul as reviewers.

### WP CLI

#23 **Develop custom WP CLI command**

Create a branch `feat/custom-cli-cmd` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. After peer approval, add Chandra and Paul as reviewers.

### Advance theme tasks

#7 **Register Sidebar Widgets**

Create a branch `feat/sidebar-widgets` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. After peer approval, add Chandra and Paul as reviewers.

#21 **Customizer options**

Create a branch `feat/customizer-options` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. After peer approval, add Chandra and Paul as reviewers.


### Gutenberg Block Tasks

Gutenberg blocks are created in a new plugin. So, the new plugin file is a dependency in both tasks. 

#8 **Custom blocks for movie post type**

Create a branch `feat/custom-movie-blocks` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. After peer approval, add Chandra and Paul as reviewers.

#20 **Custom blocks for person post type**

Create a branch `feat/custom-person-blocks` from `feat/custom-movie-blocks`. Work on this feature. Raise a PR against `feat/custom-movie-blocks` for peer code review. After peer approval, add Chandra and Paul as reviewers.

## Timeline followed for completing tasks

This is the actual timeline happened while completing tasks.

Create a branch develop from main.

### Basic Plugin Tasks

#1 **Register Custom Post Types and Taxonomies**

Create a branch `feat/cpt` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review.

#2 **Register Custom Meta Box Movie Post Type Metadata**

Create a branch `feat/movie-metadata` from `feat/cpt`. Work on this feature. Raise a PR against `feat/cpt` for peer code review. 

#3 **Register Custom Meta Box Person Post Type Metadata**

Create a branch `feat/person-metadata` from `feat/movie-metadata`. Work on this feature. Raise a PR against `feat/movie-metadata` for peer code review.

#18 **Register Custom Meta Box for Photo and Video Gallery**

Create a branch `feat/gallery-metabox` from `feat/person-metadata`. Work on this feature. Raise a PR against `feat/person-metadata` for peer code review.

#4 **Register Shortcodes**

Create a branch `feat/shortcodes` from `feat/gallery-metabox`. Work on this feature. Raise a PR against `feat/gallery-metabox` for peer code review.

#5 **Register Settings Page**

Create a branch `feat/plugin-settings` from `feat/gallery-metabox`. Work on this feature. Raise a PR against `feat/gallery-metabox` for peer code review.

Merge `feat/shortcodes` to `feat/gallery-metabox`. Merge `feat/plugin-settings` to `feat/gallery-metabox`.

Merge `feat/gallery-metabox` to `feat/person-metadata`.

Merge `feat/person-metadata` to `feat/movie-metadata`.

Merge `feat/movie-metadata` to `feat/cpt`.

Merge `feat/cpt` to `develop`.

Here, basic plugin assignment is completed and `develop` branch has the basic plugin assignment tasks. So, create a branch `feat/plugin` from develop and raise a PR from `feat/plugin` against `main` for code review by Chandra. Address feedbacks in this PR and branch `feat/plugin`.

### Basic theme tasks

#14 **Create Child theme**

Create a branch `feat/child-theme` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review.

#9 **Single Page Template - Movie**

Create a branch `feat/single-page-movie` from `feat/child-theme`. Work on this feature. Raise a PR against `feat/child-theme` for peer code review.

#10 **Archive Page Template - Movie**

Create a branch `feat/archive-page-movie` from `feat/single-page-movie`. Work on this feature. Raise a PR against `feat/single-page-movie` for peer code review.

#11 **Single Page Template - Person**

Create a branch `feat/single-page-person` from `feat/archive-page-movie`. Work on this feature. Raise a PR against `feat/archive-page-movie` for peer code review.

#12 **Archive Page Template - Person**

Create a branch `feat/archive-page-person` from `feat/single-page-person`. Work on this feature. Raise a PR against `feat/single-page-person` for peer code review.

Merge feat/archive-page-person to feat/single-page-person.
Merge feat/single-page-person to feat/archive-page-movie.
Merge feat/archive-page-movie to feat/single-page-movie.
Merge feat/single-page-movie to feat/child-theme.
Merge feat/child-theme to develop.

Here, basic theme assignment is completed and `develop` branch has the basic theme assignment tasks. So, create a branch `feat/theme` from develop and raise a PR from `feat/theme` against `feat/plugin` as `feat/plugin` has not been approved. Add Chandra & Paul for code review. Address feedbacks in this PR and branch `feat/theme`.

### Advance Plugin Tasks
#6 **Add Dashboard Widgets**

Create a branch `feat/dashboard-widgets` from `feat/plugin`. Work on this feature. Raise a PR against `feat/plugin` for peer code review. After peer approval, add Chandra and Paul as reviewers.

#16 **Create custom user role**

Create a branch `feat/custom-user-role` from `feat/plugin`. Work on this feature. Raise a PR against `feat/plugin` for peer code review. After peer approval, add Chandra and Paul as reviewers.

#17 **Add rewrite rules/permalink structure for custom post types**

Create a branch `feat/custom-rewrite-rules` from `feat/plugin`. Work on this feature. Raise a PR against `feat/plugin` for peer code review. After peer approval, add Chandra and Paul as reviewers.

#19 **Create custom database tables**

Create a branch `feat/custom-db-tables` from `feat/plugin`. Work on this feature. Raise a PR against `feat/plugin` for peer code review. After peer approval, add Chandra and Paul as reviewers.

### REST API

#22 **Create custom REST API endpoints**

Create a branch `feat/custom-rest-endpoints` from `feat/plugin`. Work on this feature. Raise a PR against `feat/plugin` for peer code review. After peer approval, add Chandra and Paul as reviewers.

#23 **Develop custom WP CLI command**

Create a branch `feat/custom-cli-cmd` from `feat/plugin`. Work on this feature. Raise a PR against `feat/plugin` for peer code review. After peer approval, add Chandra and Paul as reviewers.

At this point, my `feat/plugin` branch got approval from Chandra and Paul. So, merged basic plugin tasks PR(`feat/plugin`) to `main` and synced up `main` to `develop`.
Also, `feat/theme` got approval from Chandra and Paul. So, changed base branch from `feat/plugin` to `main` and merged `feat/theme` to `main`. Here, again synced `develop` to `main`.

Now, changing base branch to `main` and merged approved #16, #17, #19, #22, #23 to `main`.

### Advance theme tasks

#7 **Register Sidebar Widgets**

Create a branch `feat/sidebar-widgets` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. After peer approval, add Chandra and Paul as reviewers.

#21 **Customizer options**

Create a branch `feat/customizer-options` from `feat/sidebar-widgets`. Work on this feature. Raise a PR against `feat/sidebar-widets` for peer code review. After peer approval, add Chandra and Paul as reviewers.

Merge `feat/customizer-options` to `feat/sidebar-widgets`.
Merge `feat/sidebar-widgets` to `develop`.

### Gutenberg Block Tasks

#8 **Custom blocks for movie post type**

Create a branch `feat/custom-movie-blocks` from `develop`. Work on this feature. Raise a PR against `develop` for peer code review. After peer approval, add Chandra and Paul as reviewers.

#20 **Custom blocks for person post type**

Create a branch `feat/custom-person-blocks` from `feat/custom-movie-blocks`. Work on this feature. Raise a PR against `feat/custom-movie-blocks` for peer code review. After peer approval, add Chandra and Paul as reviewers.
