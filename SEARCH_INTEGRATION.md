# MiniSearch Integration for Versoris TEI-XML Project

## Overview

This document describes the MiniSearch integration added to the Bibliotheca Manuscripta Versoriana project, which provides full-text search capabilities for TEI-XML manuscripts and persons data.

## ✅ Implementation Complete

### What's been added:

1. **MiniSearch Library** - Added to all HTML pages via CDN
2. **Search UI** - Search bar in navigation on all pages
3. **Search Engine** (`js/search.js`) - Comprehensive indexing and search functionality
4. **Search Results Page** (`search.html`) - Dedicated page for displaying search results

## Key Features

- **Full-text search** across manuscripts and persons
- **Fuzzy matching** for historical spellings and variations
- **Live search suggestions** as you type
- **Field-specific search** with relevance scoring
- **Filter by type** (manuscripts vs. persons)
- **Cross-references** between manuscripts and persons
- **Clean, responsive UI** integrated with your Bootstrap theme

## How it Works

- Indexes TEI data from `mss.xml` and `PersonRegister.xml`
- Extracts titles, names, dates, places, content, and notes
- Provides instant search with autocomplete suggestions
- Results link directly to manuscript/person entries
- Search from any page navigates to dedicated results page

## Search Capabilities

The search engine can find:

- **Author names** (e.g., "Versor", "Johannes")
- **Manuscript locations** (e.g., "Paris", "Bologna")
- **Dates and time periods** (e.g., "1400", "15th century")
- **Person roles** (e.g., "scribe", "former owner")
- **Full content search** across all TEI text
- **Repository information** (libraries, collections)
- **Material descriptions** (parchment, paper)
- **Manuscript identifiers** (shelfmarks, call numbers)

## Technical Details

### Files Modified/Added:

1. **`js/search.js`** - Main search engine class
   - `VersorisSearch` class with indexing and search methods
   - TEI-XML data extraction functions
   - Search suggestion and result handling

2. **`search.html`** - Dedicated search results page
   - Advanced search interface
   - Results display with filtering
   - Search tips and navigation

3. **All HTML pages** - Updated with:
   - MiniSearch CDN script
   - Search form in navigation
   - Integration with search.js

### Search Index Structure

#### Manuscripts Index:
- `id`, `title`, `repository`, `settlement`, `idno`
- `origDate`, `origPlace`, `material`
- `author`, `content`, `notes`

#### Persons Index:
- `id`, `name`, `persName`, `birth`, `death`
- `occupation`, `note`, `idno`

### Search Options:

- **Fuzzy matching**: 0.2 tolerance for typos and variations
- **Prefix search**: Matches partial words
- **Boost weights**: Title/name (3x), author/occupation (2x), content (1.5x)
- **Cross-references**: Links between manuscripts and persons

## Usage Examples

### Basic Search:
- Type in navigation search bar
- Get live suggestions as you type
- Click suggestion or press Enter for full results

### Advanced Search:
- Visit `/search.html`
- Use filters (manuscripts only, persons only)
- View detailed results with relevance scores

### Search Query Examples:
- `"Johannes Versor"` - Find author references
- `"Paris"` - Find manuscripts in Paris
- `"scribe"` - Find persons who were scribes
- `"1450"` - Find 15th century materials
- `"parchment"` - Find manuscripts on parchment

## Performance

- **Client-side**: No server required, works offline
- **Fast indexing**: Builds search index on page load
- **Lightweight**: MiniSearch is only 2KB gzipped
- **Responsive**: Live suggestions with 300ms debounce

## Integration with CETEIcean

The search integration works seamlessly with your existing CETEIcean setup:

- Extracts data from TEI elements after CETEIcean processing
- Preserves existing navigation and cross-reference functionality
- Maintains Bootstrap styling and responsive design
- Compatible with existing TEI behaviors and custom CSS

## Browser Compatibility

- Modern browsers with ES6 support
- Works with your existing Bootstrap 5 and CETEIcean setup
- No additional dependencies beyond MiniSearch CDN

## Search Highlighting

The search system includes comprehensive **in-page highlighting** functionality that highlights search terms directly within the TEI documents:

### How Highlighting Works:

1. **URL-based activation**: Add `?highlight=term` to any page URL to highlight terms
2. **Automatic highlighting**: Search results can link with highlighting enabled
3. **Smart text detection**: Uses TreeWalker to find text nodes while preserving TEI structure
4. **Multi-term support**: Highlights multiple search terms simultaneously
5. **Visual feedback**: Shows highlight indicator with term count and clear option

### Highlighting Features:

- **Non-destructive**: Preserves original TEI markup and CETEIcean processing
- **Case-insensitive**: Matches terms regardless of capitalization
- **Auto-scroll**: Automatically scrolls to first highlighted term
- **Visual indicator**: Fixed position indicator showing search terms and match count
- **Easy clearing**: One-click button to remove all highlights
- **TEI-aware**: Waits for CETEIcean content to load before applying highlights

### Usage Examples:

- `manuscripts.html?highlight=Johannes` - Highlights "Johannes" in manuscripts
- `persons.html?highlight=scribe` - Highlights "scribe" in person records
- `search.html?q=Paris&highlight=Paris` - Search for "Paris" with highlighting

### Technical Implementation:

The `TextHighlighter` class (`js/search.js:440-693`) provides:

- **highlightSearchTerms()**: Main highlighting function
- **clearHighlights()**: Removes all highlight markup
- **Auto-detection**: Checks URL parameters on page load
- **Smart delays**: Waits for TEI content loading with exponential backoff

### CSS Styling:

Highlights use `<mark class="search-highlight">` elements with visual styling that integrates with the Bootstrap theme.

## Future Enhancements

Additional improvements could include:

- **Advanced filters** (date ranges, material types)
- **Search history** and saved searches
- **Export search results** functionality
- **API endpoints** for external search integration
- **Contextual highlighting** (showing surrounding text in results)

## Maintenance

The search functionality is self-contained and requires minimal maintenance:

- Search indices rebuild automatically on page load
- No server-side components to maintain
- Updates automatically when TEI data changes
- Error handling for network issues and missing data

---

*MiniSearch integration completed for the Bibliotheca Manuscripta Versoriana project*