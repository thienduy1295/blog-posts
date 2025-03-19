---
title: Modularize gitlab CI pipeline
date: 2025-03-19
---

# Modularize GitLab CI Pipeline

This MR implements a modular structure for our GitLab CI/CD pipeline to improve maintainability and scalability, while preserving all existing functionality.

# Changes:

- Restructured the monolithic `.gitlab-ci.yml` into modular components
- Created separate files for each pipeline stage in `.gitlab/ci/` directory
- Preserved all original script commands to ensure functionality is maintained
- Implemented a clean main configuration file that includes all modular components

# Benefits:

- Improved Maintainability: Each stage is defined in its own file, making it easier to maintain
- Better Organization: Pipeline components are logically grouped by stage
- Enhanced Readability: The main `.gitlab-ci.yml` file is now much shorter and easier to understand
- Increased Scalability: New stages or jobs can be added without cluttering the main file

# Implementation Details:

- Created `.gitlab/ci/default.yml` for common settings, variables, and stage definitions
- Separated each stage into its own file (install.yml, bot-review.yml, etc.)
- Maintained all original script commands to ensure no functionality is lost
- Main `.gitlab-ci.yml` now only includes the modular components

This modular approach follows GitLab CI/CD best practices and will make future pipeline changes easier to implement and maintain.
