# Render Mermaid Diagrams with Embedded Images (Ditch Mermaid CDN)

### Earlier Approach (Complicated Method)

Previously, we used a more complex method involving Mermaid CDN and custom JavaScript logic to render Mermaid diagrams, shown below:

```html
<script type="module">
      import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';
      mermaid.initialize({ startOnLoad: false }); // Prevent automatic rendering
      document.addEventListener('DOMContentLoaded', function() {
          // Find all code blocks with class 'mermaid'
          const mermaidBlocks = document.querySelectorAll('pre code.language-mermaid');
          mermaidBlocks.forEach(block => {
              const code = block.textContent; // Get the content of the code block
              const mermaidDiv = document.createElement('div');
              mermaidDiv.classList.add('mermaid');
              mermaidDiv.textContent = code; // Set the content to the div
              block.parentNode.replaceChild(mermaidDiv, block); // Replace code block with div
          });
          mermaid.init(); // Render all mermaid diagrams
      });
</script>
```

### What's the Better Approach Now?

Instead of doing the above, you can follow this **simple method** using Mermaid Ink. Just:

1. Read and follow these [four steps](https://mermaid.ink/).
2. Apply them.

### How to Make a Clickable Link Out of the Embedded Image?

1. **Copy the original embedded link** that starts with `mermaid-js.github.io`.
2. **Take the part after the `#`** in the link and **concatenate it after**: `https://mermaid.ink/img/`.
3. This new `mermaid.ink` link becomes the URL for the embedded image.
   > **Note:** This is called an "embedded" image because it is being served from an external source (the internet), rather than being uploaded directly to your server.
4. You'll now have a link like this:

   ```
   https://mermaid.ink/img/pako:eNo9UL1ugzAQfpXTTY2UCDXkr6jKlK7tkC4Vx3CAG1CCjRxbagqsnfuMfZIaQ9i-f-muwUzlAiM8aa4LeD-QfHyIj4a1SWawWOxhGRMy_P38wtdzqoM9pJ7cPMk8_vaYMCG59J2wYXDBjmTY8_ZDXFtYeTFz4sqHBnUTB2_W1NYAB8lota-qhd1kZL0RTsa6Sced9bDj0xPzq9upnPblrbee-sNUncxIbgaB5O4OcI6V0BWXuXtGQxKA0BSiEoSRgznrMyHJzuXYGnW8yQwjo62Yo1b2VGD0yZerY7bO2YhDye6j1T0yiC95aZQek90_HeB4Xg
   ```

5. Embed this link into Markdown like so:

   ```markdown
   ![alt-text](https://mermaid.ink/img/pako:eNo9UL1...)
   ```

6. **Make the Image Clickable** by wrapping it in another Markdown link:

   ```markdown
   [![](https://mermaid.ink/img/pako:eNo9UL1...)](https://mermaid-js.github.io/...)
   ```

7. **Commit and Enjoy!**

### A Note About Using Only the `mermaid-js.github.io` Link

If you prefer to use the original `mermaid-js.github.io` link directly inside the `![]()` Markdown syntax, you'll need to implement additional JavaScript logic or use templating (e.g., with Hugo) to render the image.

### Here is the additional Javascript code:

Absolutely! We can modify the JavaScript code to make the rendered Mermaid diagrams clickable. This can be achieved by wrapping the `<img>` elements in anchor (`<a>`) tags that link back to the original `mermaid-js.github.io` URL.

### Updated JavaScript Code for Clickable Images

Here’s the updated script that wraps each Mermaid image in a clickable link:

```html
<script type="module">
    document.addEventListener('DOMContentLoaded', function () {
        // Find all image elements in the document
        const images = document.querySelectorAll('img');

        // Loop through each image
        images.forEach(img => {
            const src = img.src;

            // Check if the src contains 'mermaid-js.github.io'
            if (src.includes('mermaid-js.github.io')) {
                // Extract the encoded string after the '#' in the URL
                const encodedString = src.split('#')[1];

                // Create the new Mermaid Ink URL
                const mermaidInkURL = `https://mermaid.ink/img/${encodedString}`;
                
                // Create the original link
                const originalLink = src;

                // Create an anchor element
                const anchor = document.createElement('a');
                anchor.href = originalLink;  // Set the href to the original link
                anchor.target = '_blank';  // Open link in a new tab

                // Replace the image src with the Mermaid Ink URL
                img.src = mermaidInkURL;

                // Append the image to the anchor
                anchor.appendChild(img.parentNode.replaceChild(anchor, img));
            }
        });
    });
</script>
```

### How This Updated Script Works:

1. **Finds all `<img>` elements**: The script searches for all images in the document.
2. **Checks the image `src`**: It checks whether the `src` contains the string `mermaid-js.github.io`.
3. **Extracts the encoded string**: If found, it takes the part after the `#` in the `mermaid-js.github.io` URL.
4. **Creates the new Mermaid Ink URL**: It constructs the URL to load the image from Mermaid Ink.
5. **Creates an anchor (`<a>`) element**: It creates a clickable link that points back to the original `mermaid-js.github.io` link.
6. **Replaces the `src`**: It replaces the `src` of the `<img>` with the new Mermaid Ink URL.
7. **Wraps the image in the anchor tag**: Finally, it wraps the image in the anchor element, making it clickable.

### Example Markdown Usage

With the above script, you can use a Mermaid diagram link like this in your Markdown:

```markdown
![Mermaid Diagram](https://mermaid-js.github.io/mermaid-live-editor/edit#pako:eNo9UL1ugzAQfpXTTY2UCDXkr6jKlK7tkC4Vx3CAG1CCjRxbagqsnfuMfZIaQ9i-f-muwUzlAiM8aa4LeD-QfHyIj4a1SWawWOxhGRMy_P38wtdzqoM9pJ7cPMk8_vaYMCG59J2wYXDBjmTY8_ZDXFtYeTFz4sqHBnUTB2_W1NYAB8lota-qhd1kZL0RTsa6Sced9bDj0xPzq9upnPblrbee-sNUncxIbgaB5O4OcI6V0BWXuXtGQxKA0BSiEoSRgznrMyHJzuXYGnW8yQwjo62Yo1b2VGD0yZerY7bO2YhDye6j1T0yiC95aZQek90_HeB4Xg)
```

### Result:
- The image will be rendered from the `mermaid.ink` link.
- Clicking on the image will take the user to the original `mermaid-js.github.io` link in a new tab.

This way, you get both a rendered image and a clickable link to the original Mermaid editor. 

### One more things before you leave

You wont have to copy paste this script tag in all your converted HTML(if you use pandoc)
but Hugo will automatically do it everytime we convert our markdown to html, as we will make a template once as resuse it.

one more thing we dont even have to convert each file individually, hugo will be put inside a workflow that would trigger Hugo when any markdown file is updated.

### Pandoc Destroyed. Mic Drop. Peace.
