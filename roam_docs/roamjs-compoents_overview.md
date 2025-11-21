# RoamJS Components Library Overview

This document provides a comprehensive overview of the modules and components available in the RoamJS Components library, a collection of utilities and React components for developing extensions for Roam Research.

## Components (`src/components`)

This directory contains reusable React components designed to integrate seamlessly with the Roam Research UI.

### AutocompleteInput.tsx
Implements a generic autocomplete input field. It is highly customizable, supporting various options, multiline input, and fuzzy search for filtering. The component manages its own state, handles keyboard navigation, and displays a popover menu with selectable options, including support for creating new items.

### BlockErrorBoundary.tsx
A React error boundary component designed for wrapping custom components rendered in Roam blocks. If an error occurs within its children, it catches the error, logs it by creating a new block in Roam with an error message, and then displays a fallback UI.

### BlockInput.tsx
Provides a specialized search input for finding Roam Research blocks. As a user types, it uses regex to search all blocks and displays a menu of matching results. It supports selection via keyboard or mouse and is ideal for quick block referencing in forms or dialogs.

### ComponentContainer.tsx
A wrapper component that adds editing functionality to its children when hovered. It can focus and select the underlying Roam block when an edit icon is clicked. This is often used to embed custom components into Roam blocks while providing additional UI controls.

### ConfigPage.tsx
The main configuration page component for RoamJS extensions. It supports both legacy and new configuration structures, renders various field types and tabs, and manages the enabling and disabling of features. It also includes utilities for rendering and observing configuration pages, allowing for dynamic updates.

### CursorMenu.tsx
Implements a popover menu that appears at the cursor's position within a textarea. It allows users to select from a list of filtered options, using fuzzy search and keyboard navigation. The component integrates with Roam block updates and is useful for features like autocomplete or user mentions.

### Description.tsx
Renders a small info icon that displays a descriptive tooltip on hover. This component is used to annotate UI elements with additional context or help text in a styled tooltip.

### ExtensionApiContext.tsx
Provides a React context for accessing the RoamJS extension API and its version. It includes hooks that allow any component in the tree to consume the API and version information. This component is marked as deprecated in favor of a utility in another directory.

### ExternalLogin.tsx
Handles OAuth and other external authentication workflows. It manages pop-out login windows, state, and authentication data, with support for both local and remote account storage. The component displays the login UI, handles success and error states, and integrates with Roam blocks for storing credentials.

### Filter.tsx
Implements a user interface for building complex filters with "includes" and "excludes" logic across multiple categories. It supports fuzzy search, toggling filters, and displays the active filter state with color cues. It is used to filter data sets in UI views, such as tables or search results.

### FormDialog.tsx
A generic dialog component for creating forms. It supports a wide variety of field types, including text, number, select, page, block, autocomplete, checkbox (flag), and embeddable content. The dialog handles field dependencies, conditional rendering, asynchronous submission, and is deeply integrated with Roam for fetching block and page data. It also includes utility methods for rendering overlays and prompting for user input.

## DOM Utilities (`src/dom`)

This directory provides a collection of utility functions and constants for interacting with the Document Object Model (DOM) within Roam Research. These helpers enable developers to manipulate the UI, observe changes, and work with Roam-specific data attributes.

### Key Functionalities

*   **Adding Block Commands & Script Dependencies**:
    *   `addBlockCommand`: Adds a new command to the command palette for a specific block.
    *   `addRoamJSDependency`, `addOldRoamJSDependency`, `addScriptAsDependency`: Manage and ensure required scripts are loaded for an extension to function correctly.

*   **DOM Observation & Manipulation**:
    *   `createBlockObserver`, `createHTMLObserver`, `createPageTitleObserver`, `createButtonObserver`, `createDivObserver`, `createOverlayObserver`: A suite of functions that use `MutationObserver` to monitor changes to specific parts of the Roam DOM and trigger callback functions.

*   **Retrieving & Manipulating Roam-Specific Data**:
    *   `getCurrentPageUid`, `getBlockUidFromTarget`, `getUids`, `getUidsFromId`, `getActiveUids`: Functions to retrieve unique identifiers (UIDs) for pages and blocks from various DOM elements and contexts.

*   **URL Generation & Reference Resolution**:
    *   `getRoamUrl`, `getRoamUrlByPage`: Generate sharable URLs for specific Roam pages or blocks.
    *   `resolveRefs`: Resolves Roam-style block references or aliases to their corresponding URLs or content.

*   **Parsing Roam Block Content**:
    *   `parseRoamBlocksToHtml`: Converts the content of Roam blocks from Roam's format into standard HTML, which is useful for exporting or custom rendering.

*   **Utility Functions**:
    *   `getReferenceBlockUid`: Finds the UID of a referenced block from a given DOM element.
    *   `addStyle`: Injects a string of CSS styles into the document's head.
    *   `createIconButton`: A helper to generate icon buttons that match Roam's UI style.
    *   `elToTitle`, `getPageTitleValueByHtmlElement`: Extract the title or text content from DOM nodes.
    *   `getDropUidOffset`: Calculates the parent UID and drop offset for elements that are dragged and dropped in the UI.
    *   `getMutatedNodes`: Works with and identifies nodes that have been changed in the DOM.

*   **Constants**:
    *   `BLOCK_REF_REGEX`: A regular expression for identifying block references in Roam.
    *   Other constants are provided for various DOM operations.

## Event Handling (`src/events`)

This directory centralizes utilities for setting up and managing event listeners in Roam Research. It allows developers to respond to changes within the application's data model.

### Key Functionalities

*   **`watchOnce`**:
    *   This function sets up a one-time watcher on a specific Roam Research block.
    *   It listens for changes that match a given `pullPattern` and a specific block ID (`entityId`).
    *   When a matching change is detected, it executes a callback function with the state of the data before and after the change.
    *   If the callback function returns `true`, the watcher automatically removes itself.
    *   This is particularly useful for cases where an action should only be triggered once, such as updating a visualization or sending a notification after a specific block is updated.

## Date Utilities (`src/date`)

This directory provides helper functions for parsing and manipulating dates and times, which is essential for any feature that interacts with Roam's daily notes or date-based data.

### Key Functionalities

*   **Natural Language Date Parsing**:
    *   `parseNlpDate`: Uses the `chrono-node` library to interpret natural language date strings (e.g., "yesterday," "next Friday"). It also includes custom refinements for phrases like "start of week" or ordinal weekdays in a month (e.g., "first Monday of June").

*   **Roam Date UID Parsing**:
    *   `parseRoamDateUid`: Converts a Roam Research date UID (which follows a "month-date-year" format) into a standard JavaScript `Date` object.

*   **Constants**:
    *   `MONTHS`: An array containing the names of the months.
    *   `DAILY_NOTE_PAGE_REGEX` and `DAILY_NOTE_PAGE_TITLE_REGEX`: Regular expressions used for matching and validating the titles of daily note pages.

## React Hooks (`src/hooks`)

This directory contains custom React hooks for managing user interactions and complex data structures within RoamJS extensions.

### Key Functionalities

*   **`useArrowKeyDown`**: Handles keyboard navigation for lists (like autocomplete menus). It tracks the active item index and provides logic for `ArrowDown`, `ArrowUp`, and `Enter` key presses to cycle through and select items.
*   **`useSubTree`**: Manages sub-tree data structures from Roam blocks. It uses React's `useMemo` hook to efficiently compute and update the sub-tree data based on dependencies like a parent UID, returning the current sub-tree and a function to update it.

## Markdown Parsing (`src/marked`)

This directory provides customized Markdown parsing and rendering for Roam Research, building upon the `marked` library to handle Roam-specific syntax and elements.

### Key Functionalities

*   **Language Syntax Highlighting**: Uses the `refractor` library to provide syntax highlighting for various languages in code blocks.
*   **Custom Regular Expressions**: Defines regex patterns for Roam-specific elements like `[[TODO]]`/`[[DONE]]`, block references, tags, aliases, and attributes.
*   **Custom Renderer**: Extends the `marked` renderer to correctly handle Roam-specific links, aliases, tags, and other custom elements.
*   **Contextual Parsing**: Allows Markdown parsing to adapt to Roam-specific page and block references, providing context-aware parsing functions.

## Database Queries (`src/queries`)

This directory provides utility functions for querying and interacting with the Roam Research database. These functions enable data retrieval, manipulation, and normalization.

### Key Functionalities

*   **Block & Page Retrieval**: Functions like `getAllBlockUids`, `getAllPageNames`, and `getFullTreeByParentUid` retrieve lists of blocks, pages, and their hierarchical data.
*   **Attribute & Metadata Extraction**: `getAttributeValueByBlockAndName` retrieves the value of a specific attribute from a block using Datalog queries. Other utilities extract various metadata.
*   **Tag & Reference Utilities**: Helpers for checking tag existence on a page (`isTagOnPage`) and working with block relationships.
*   **Datalog Compilation**: `compileDatalog` converts Datalog query objects into the string format required to query Roam’s database.
*   **Page Title Normalization**: `normalizePageTitle` escapes and standardizes page titles to ensure they can be safely used in queries.

## Scripts (`src/scripts`)

This directory contains scripts for managing RoamJS extension publishing and development workflows, including command-line utilities.

### Key Functionalities

*   **CLI Entry Point**: The `index.ts` file serves as the command-line interface entry point for building, testing, and deploying RoamJS extensions.
*   **Extension Publishing Automation**: `publishToRoamDepot.ts` automates publishing an extension to the Roam Depot. It handles checking for existing pull requests, cloning the depot repository, updating the extension manifest, and creating or updating pull requests on GitHub.

## Type Definitions (`src/types`)

This directory defines the core TypeScript types and interfaces for the RoamJS extension ecosystem, ensuring type safety across the library.

### Key Functionalities

*   **Centralized Type Definitions**: A main index file exports types from various submodules. A central `Registry` type manages state for listeners, commands, and other extension elements.
*   **Roam Research Data Structures**: Models for `RoamBasicBlock`, `RoamBasicPage`, and other core Roam data structures.
*   **Datalog and Query Builder Types**: Types for modeling Datalog queries and their results.
*   **SmartBlocks & Client-Side Actions**: Definitions for SmartBlocks commands and parameters for client-side actions like creating or updating blocks.
*   **User Settings and Sidebar**: Types for modeling user settings and sidebar UI components.
*   **Global Window Extensions**: Extends the global `Window` object to include the `roamAlphaAPI` and the `roamjs` namespace for cross-extension communication.

## Utility Functions (`src/util`)

This directory provides a comprehensive set of utility functions that support almost all aspects of RoamJS extension development.

### Key Functionalities

*   **API Interaction**: Standardized functions for HTTP requests (`apiGet`, `apiPost`) and OAuth management.
*   **DOM and Rendering**: Helpers for rendering overlays (`createOverlayRender`) and working with the DOM in Roam.
*   **Data Extraction and Transformation**: Utilities to extract data from Roam content, such as references (`extractRef`) and tags (`extractTag`).
*   **Settings and Configuration**: Functions to manage extension settings (`addInputSetting`, `getSettingValueFromTree`).
*   **Extension Management**: Helpers to manage the extension lifecycle, including setup, cleanup, and deprecation warnings.
*   **Miscellaneous Utilities**: Low-level helpers for tasks like DOM checks and web worker interactions.

## Database Writes (`src/writes`)

This directory contains functions for performing write operations on the Roam Research database, such as creating, updating, and deleting content.

### Key Functionalities

*   **Block Operations**:
    *   `createBlock`, `updateBlock`, `deleteBlock`: Create, modify, or remove a block by its UID.
    *   `clearBlockById`/`clearBlockByUid`: Clear the content of a block.
    *   `updateActiveBlock`: Update the content of the currently focused block.
*   **Page Operations**:
    *   `createPage`: Creates a new page, with support for daily note UID generation.
*   **Sidebar Operations**:
    *   `openBlockInSidebar`: Opens a specific block in the right sidebar.
*   **Action Submission**: All write operations use a central `submitActions` function that queues actions and includes built-in retry logic to ensure reliable API interactions.