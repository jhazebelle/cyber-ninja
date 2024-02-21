// Tried two fixes as follows:
///////////////////////////////////////////////////////////////////////////////////////////////
// 1. I implemented the DOMContentLoaded event into the content script code, and
// needed to wrap the existing logic inside an event listener for the DOMContentLoaded event. 
//////////////////////////////////////////////////////////////////////////////////////////////
// Listen for the DOMContentLoaded event
document.addEventListener('DOMContentLoaded', function() {
    // Your content script logic goes here
    const article = document.querySelector("article");
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
});
/////////////////////////////////////////////////////////////////////////////////////
// 1. This did not work so I implemented document.readyState to check if the document is fully loaded before executing the content script logic.
////////////////////////////////////////////////////////////////////////////////////
// 2. 

// Check if the document is already in the "complete" state
if (document.readyState === 'complete') {
    executeContentScriptLogic();
} else {
    // If the document is not yet in the "complete" state, wait for the "readystatechange" event
    document.addEventListener('readystatechange', function() {
        if (document.readyState === 'complete') {
            executeContentScriptLogic();
        }
    });
}

function executeContentScriptLogic() {
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
}

// 2. This also did not work. 
