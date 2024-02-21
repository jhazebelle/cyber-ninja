// When completing Step 4 of Google's tutorial "Run scrip on every page", and adding the URLs for "Chrome DevTools" and
// "Workbox" to the manifest file, we are given a TypeError in our reading-time extension, located in Manage Extensions in Chrome.

// The error is as follows:

// Uncaught TypeError: Cannot read properties of null (reading 'insertAdjacentElement')
// Context
// https://developer.chrome.com/docs/devtools/
// Stack Trace
// scripts/content.js:21 (anonymous function)

// This is from line 1 to line 22
        const article = document.querySelector("article");

// `document.querySelector` may return null if the selector doesn't match anything.
if (article) {
  const text = article.textContent;
  const wordMatchRegExp = /[^\s]+/g; // Regular expression
  const words = text.matchAll(wordMatchRegExp);
  // matchAll returns an iterator, convert to array to get word count
  const wordCount = [...words].length;
  const readingTime = Math.round(wordCount / 200);
  const badge = document.createElement("p");
  // Use the same styling as the publish information in an article's header
  badge.classList.add("color-secondary-text", "type--caption");
  badge.textContent = `⏱️ ${readingTime} min read`;

  // Support for API reference docs
  const heading = article.querySelector("h1");
  // Support for article docs with date
  const date = article.querySelector("time")?.parentNode;

  (date ?? heading).insertAdjacentElement("afterend", badge);
}

// The fixed code is as follows:

const article = document.querySelector("article");

// Check if the article element exists
if (article) {
  const text = article.textContent;
  const wordMatchRegExp = /[^\s]+/g; // Regular expression
  const words = text.matchAll(wordMatchRegExp);
  // matchAll returns an iterator, convert to array to get word count
  const wordCount = [...words].length;
  const readingTime = Math.round(wordCount / 200);
  const badge = document.createElement("p");
  // Use the same styling as the publish information in an article's header
  badge.classList.add("color-secondary-text", "type--caption");
  badge.textContent = `⏱️ ${readingTime} min read`;

  // Support for API reference docs
  const heading = article.querySelector("h1");
  const date = article.querySelector("time")?.parentNode;

  // Check if either heading or date exists before inserting the badge
  if (date || heading) {
    const insertElement = date ?? heading;
    insertElement.insertAdjacentElement("afterend", badge);
  } else {
    console.error("Neither date nor heading found.");
  }
} else {
  console.error("Article element not found.");
}

// Fixes:
// 1. Added an outer if statement to check if the article element exists before proceeding
// 2. In this same statement, we perform all the operations related to calculating reading time and creating the badge
// 3. We then check if either date or heading exists before attempting to insert the badge. If neither exists, we log an 
//   error message to the console.
