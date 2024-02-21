// This is the content script page used in Part 2 of this repository where last 2 urls in the last are not working with the
// chrome extension unless the page is reloaded

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
