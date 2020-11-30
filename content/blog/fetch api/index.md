---
title: Project - Fetch API
date: "2020-11-29"
description: "Simple project to learn Fetch API featuring Kanye."
categories: [javascript, project]
comments: false
image:
  feature: https://miro.medium.com/max/3200/1*-yw3mCIfvJotovxiydYa1w.jpeg
---

![Fetch API](https://miro.medium.com/max/3200/1*-yw3mCIfvJotovxiydYa1w.jpeg)

Fetch API is the newer standard (compared to Ajax and XMLHttpRequest) for making HTTP requests.

This is a simple project on how to use the Fetch API for simple HTTP requests. I'll be using the free [Kanye West quotes REST API](https://kanye.rest/) for the GET requests.

If you don't need a step-by-step then go ahead and see the completed project on my GitHub [https://github.com/KevinIbay/kanye-said-what](https://github.com/KevinIbay/kanye-said-what). For preview of the final product, take a look at [https://kevinibay.github.io/kanye-said-what/](https://kevinibay.github.io/kanye-said-what/).

### Step 1 - index.html

Create the HTML file for the project.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      href="https://unpkg.com/tailwindcss@^2/dist/tailwind.min.css"
      rel="stylesheet"
    />
    <title>Kanye said what?</title>
  </head>
  <body>
    <div class="container mx-auto pt-10">
      <button
        id="newQuoteBtn"
        class="border-2 rounded-lg p-2 bg-red-300 w-full"
      >
        What did Kanye say?
      </button>
      <h1 class="text-2xl font-semibold">
        <span id="kanyeSaid" class="font-normal"
          >Don't let me get in my zone</span
        >
        - Kanye
      </h1>
    </div>
    <script src="kanye.js"></script>
    <script src="app.js"></script>
  </body>
</html>
```

### Step 2 - kanye.js

Create the JS file that will hold the Kanye class. Within Kanye, we'll create the simple fetch request.

```js
class Kanye {
  // fetch what kanye said
  async getQuote() {
    // fetch will return a response object from API
    const response = await fetch(`https://api.kanye.rest`)
    // convert response to JSON
    const responseData = await response.json()
    // the return will be a promise because the function is async
    return responseData
  }
}
```

### Step 3 - app.js

Create the main JS file that we'll be using to manipulate the HTML.

The most important part to look at here is how we consume the Promise returned by the **_kanye.getQuote()_** method with a **_.then()_** block. More on how to handle Promises returned by async functions at [MDN web docs](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await).

```js
const kanye = new Kanye()
const kanyeSaid = document.querySelector("#kanyeSaid")
const newQuoteBtn = document.querySelector("#newQuoteBtn")

newQuoteBtn.addEventListener("click", () => {
  kanye
    .getQuote()
    .then(res => (kanyeSaid.textContent = res.quote))
    .catch(err => console.log(err))
})
```

### Closing Thoughts

You probably thought at some point in the project that I didn't _need_ to use classes, async/await, and TailwindCSS in this project. However, exposure and practicing concepts that you're learning is the best way to absorb new knowledge.

> The only source of knowledge is experience. - Albert Einstein

##### Credits & References

Fetch API - https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
Promises - https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Promises
Async/Await - https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await

Asynchronous JS- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous

Kanye API - https://kanye.rest/
