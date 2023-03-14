## Images

<img src="images/tulips.png" # url of the image, could be local or website
    alt="This is supposed to be an image of tulips" text that replace the image when the image cant be visualized
    title="Tulips from woodburn tulip festival" text shown when the mouse is over the image
    height="173" in pixels
    width="262" in pixels, if width not shown, the axpect ratio will be adjusted with height. Viceversa also works
> doesnt require self closing tag.

hints: 
- don't put decorative images in your html, put them in the css.
- Add alt and title helps search engines to put your website at the top of the result.

## HyperLinks

<a href="https://en.wikipedia.org/wiki/Hyperlink"
    target="_self or _blank" _self: Same website, _blank: New window
    media="print and (resolution:250dpi)"
    download="new name"
>Click here</a> 

**href** attribute:
- Websites: https://en.wikipedia.org/wiki/Hyperlink
- Bookmarkers: https://en.wikipedia.org/wiki/Hyperlink#History
- Relative website: contacts.html
- Place in the current website: #details (it has to be added as an id in your html file)
- Protocols for emails: mailto:authors@example.com?Subject=Hello

**media** attribute:
It is used to specify what kind of media or device the URL you linked to in href is optimized for

**download** attribute:
To directly download what is in the link, if no new name was specified, it will have the same name as the file.

Using image as link:

<a href="https://www.w3.org/Style/Examples/007/leaders">
  <img src="table-th.png" alt="CSS tips related to dot leaders">
</a>

**hints:**

- Try to use text instead of images when possible
- Avoid phrases like 'Click Here' or 'Read More'. Just create it around the target 'Get Help'.
- Don't use short link text like one word.
- You should probably avoid using hyperlinks for email addresses. Bots danger and pop up default email client which the user do not use.
- the download attribute only works for same-origin URLs for security purposes

**States of Hyperlink**:

- Unvisited: blue + underlined
- Visited: purple + underlined
- Active: red + underlined


