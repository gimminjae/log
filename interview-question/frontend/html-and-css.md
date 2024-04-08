From [linked-in](https://www.linkedin.com/posts/harisahmad59_frontend-interview-questions-ugcPost-7175011891927285760-24bQ?utm_source=combined_share_message&utm_medium=member_desktop)

# HTML
### 1. What is the purpose of the `DOCTYPE` declaration in HTML?
 > The purpose of the DOCTYPE declaration is to ensure that the web browser renders the web page correctly by specifying the document type and version.
### 2. Explain the difference between `<div>` and `<span>` in HTML?
> `<div>` is a block-level element, which means it typically starts on a new line and takes up the full width available.
> It is commonly used to create sections or divisions in an HTML document.
> - `<div>` example
> ```html
> <div>
>   <h1>Main Title</h1>
>   <p>This is the main content.</p>
> </div>
> ```
> `<span>` are often used to apply CSS styles, such as color, font size, font, weight, or text decoration, to individual words or phrases within a paragraph or heading.
> They can also be used to target specific portions of text for JavaScript manipulation, such as adding event listeners or dynamically changing content.
> - `<span>` example
> ```html
> <p>This is <span style="color: red;">highlighted</span> text.</p>
> ```
>

### 3. How do you link an `external CSS stylesheet` to an HTML document?
> To link an external CSS stylesheet to an HTML document, you can use the `<link>` element in the `<head>` section of the HTML document.
>
> In the `<link>` element, there are two attributes.
> The `rel` attribute specifies the relationship between the current document and the linked resource.
> The `href` attribute specifies the path to the external CSS file. You need to provide the correct path to your CSS file here.
> - example
> ```html
> <head>    
>   <link rel="stylesheet" href="styles.css">
> </head>
> ```
### 4. What is the significance of the alt attribute in the `<img>` tag?
> 1. Accessibility <br>
> Providing descriptive and accurate alt text ensures that visually impaired users can understand the purpose and content of the image even if they cannot see it.
> 2. SEO(Search Engine Optimization) <br>
> Search Engine use `alt` text to understand the content and context of images on a web page.
> 3. Image Loading Failures <br>
> If the image fails to load due to a slow network connection, server error, or any other reason, the browser will display the `alt` text instead of the image.
### 5. Describe the difference between `GET` and `POST` methods in HTML forms.
> `GET` and `POST` differ in several aspects, including how data is transmitted and how they are handled by the server.
> 1. Data Transmission <br>
> When using the `GET`, form data is appended to the URL as a query string. This means that the form data is visible in the URL, which may pose security risks if sensitive information is being transmitted. The maximum length of a URL in most browsers is limited, so `GET` requests are typically used for submitting small amounts of data. <br>
> On the other side, with the `POST`, form data is sent as part of the HTTP request body, rather than appended to the URL. This allows for the transmission of larger amounts of data, and the data is not visible in the URL, providing better for sensitive information.
> 
> 2. Caching <br>
> `GET` can be cached by the browser and intermediaries(such as proxy servers). This means that subsequent identical requests may be served from the cache, resulting in faster page load times. However, caching can also lead to security and privacy issues if sensitive information is cached. <br>
> On the other side, `POST` requests are not cached by default. Each `POST` request is treated as a separate request by the browser and intermediaries, so data is not stored in the cache.
>
> 3. Idempotent <br>
> `GET` is idempotent, meaning that multiple identical `GET` requests will have the same effect as a single request. `GET` requests should only retrieve data and should not have any side effects on the server or the application state.<br>
> `POST` requests are not necessarily idempotent. They may have side effects on the server or the application state, such as creating or modifying data. Therefore, it is important to handle `POST` requests carefully to avoid unintended side effects.

### 6. What is the purpose of the `<meta>` tag, and how is it used?
### 7. How can you create a hyperlink that opens in a new tab or window?
### 8. What is the semantic difference between `<strong>` and `<b>`, and `<em>` and `<i>`?
### 9. Explain the concept of HTML5 semantic elements and provide examples.
### 10. How does the `<iframe>` tag work, and what is it commonly used for in HTML?
# CSS
### 1. What is the `box model in CSS` and how does it work?
### 2. Explain the difference between `margin` and `padding` in CSS.
### 3. How can you center an element horizontally and vertically in CSS?
### 4. What is the purpose of the `z-index` property in CSS?
### 5. Describe the difference between `inline` and `block-level elements` in CSS.
### 6. What is the difference between `display: none` and `visibility: hidden` in CSS?
### 7. How do media queries work in responsive web design with CSS?
### 8. Explain in the CSS selector specificity and how it affects styling.
### 9. What is the `clearfix hack`, and why is it used in CSS?
### 10. How can you include `external fonts` in a web page using CSS?
