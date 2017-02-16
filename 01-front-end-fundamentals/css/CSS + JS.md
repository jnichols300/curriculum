# CSS

##LO's
- Construct a CSS rule using selectors, declarations, properties, and values
- Articulate the pros and cons of stylesheets, styles in the head, and in-line styles
- Define "cascading" in the context of CSS specificity
- Style the size, color, border, text, and font of all elements of a given tag on a page
- Demonstrate the use of class and ID selectors to target specific element(s)
- Distinguish between block and inline display values
- Identify the components of the box model
- Differentiate between the border-box and content-box values for box-sizing
- Apply knowledge of the box model to adjust spacing between and around elements on a page
- Bookmark 2-3 good resources that developers can use refer to for CSS help


## Separation of Concerns

It is possible to style web pages using html alone. We did this in the early 2000s using mostly images and table borders. CSS allows us to separate
the styles of our website/app from the content and behavior:

- HTML
  - Content 
- CSS
  - Styles 
- JS
  - Behavior 

## In-line vs head vs stylesheets(30m)
> Not a codealong let class know they're welcome to but may be better just to pay attention to the first hour instead of typing everything out. All notes available in lesson plan

At the crux of it all, the primary concept of CSS is to select an HTML element and then do something to it. IE. I want to take the body element, and I want to apply a background color to it.

Let's get started by creating a new html webpage that we'll call `index.html` in `~/wdi/sandbox/css/`:

```bash
$ touch index.html
```

Let's throw some dummy content into HTML inside our `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>CSS!</title>
</head>
<body>
  <h1>Hello world!</h1>
  <p>This is some fake dummy content. It doesn't matter what it is! Whatever you want! Smelly fish create beautiful works of art in order to achieve world peace.</p>
  <!-- http://hipsum.co/ -->
</body>
</html>
```

*Whiteboard definitions as they come up*

So one way we can style elements in HTML is in the tag itself. These are called inline-styles:

```html
<p style="background:blue;"></p>
```

What's the best way? External stylesheets! Let's create a new file called `styles.css`:

In our `index.html` let's go ahead and link to that stylesheet in the `<head>`:

```html
<head>
  <title>CSS!</title>
  <link rel='stylesheet' href='styles.css'>
</head>
```

In `styles.css`:
```css
p{
  background:blue;
}
```

That seems like a lot more work. And you might be right initially. But we're talking about 1 `<p>` right now. What if we're talking about 100 `<p>`'s and now those elements were spread across multiple web pages. Now all of a sudden this last method is less work.

## CSS Selectors(10m)
As you can see, there's more than one place to target elements. There's also multiple WAYS you can target elements. Let's throw some additional content in `index.html`:

```html
<body>
  <h1>Hello world!</h1>
  <p>This is some fake dummy content. It doesn't matter what it is! Whatever you want! Smelly fish create beautiful works of art in order to achieve world peace.</p>
  <p class="red">This paragraph tag element has a class of "red"</p>
  <p class="red" id="green">This paragraph tag element has an id of "green"</p>
  <div class="red">This div tag element has a class of "red"</div>
</body>
```

All I did here was add two `<p>` elements and added a class of "red" to both and an id of "green" to the last. Additionally I added a `<div>` element with a class of red.

The first thing I want to do is make it so all elements with the class of "red" has a background of red. In our `styles.css`:

```css
.red {
  background: red;
}
```

Awesome, but I think I want just the `<p>` elements with that class name to have a background of red. So in `styles.css`:

```css
p.red{
  background: red;
}
```

Finally to select an element with an id you use `#`. I'm going to change the background color of the p element with class "green" in our `styles.css`:

```css
#green{
  background: green;
}
```

*whiteboard common selectors as well as let them know about references at the bottom of the page*

## CSS Specificity (20m)
If I change the css selector from `p.red` back to `.red` you'll notice that the paragraph element with the id of green is still green. This is because of CSS Specificity. While CSS cascades from top to bottom. The CSS that is applied depends on Specificity as well. Take the following example:

```css
#green {
  background: green;
}
.red {
  background: blue;
}

.red {
  background: red;
}
```

In this example the elements that have the class red, will ultimately have a background of red even though blue was set first because it takes the last declared property. However, even though the `#green` selector was written first, it has a higher specificity and therefore overides the following background properties.

The following list of selector types is by increasing specificity:

- Universal selectors (e.g., '\*')
- Type selectors (e.g., h1)
- Class selectors (e.g., .example)
- Attributes selectors (e.g., [type="radio"])
- Pseudo-classes (e.g., :hover)
- ID selectors (e.g., #example)
- Inline style (e.g., style="font-weight:bold")

You can read more about CSS specificity [here](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)
You can access a CSS specificty calculator [here](http://specificity.keegan.st)

## The Box Model!(15m)
> One of the tricky things about CSS at first is the Box Model. But it's actually really simple. Let's break it down.

![](https://dl.dropboxusercontent.com/s/capg35hblhr6o7v/Screenshot%202015-10-13%2014.11.39.png?dl=0)

Any HTML element can be considered a box, and so the box model applies to all HTML elements. If you select an element prescribe it a height and width, the content itself will be that height and width.

What the size doesn't include:
- padding
- border
- margin

Let's go into our existing `index.html` and `styles.css` and add some stuff to illustrate what I mean. In `index.html`:

```html
<p>This is a paragraph</p>
<p class="padding">This is a paragraph</p>
```

In `styles.css`:

```css
p {
  background: red;
  height: 100px;
  width: 20%;
}
```

Lets check this out in our chrome browser with the developer tools. As you can see, everything is identical. Which makes sense. Let's go ahead and add some padding to the html element with class "padding". In `styles.css`:

```css
p {
  background: red;
  height: 100px;
  width: 20%;
}

p.padding {
  padding:10px;
}
```

> Well that's certainly interesting. Even though the dimensions are the same. The element with padding is larger.

Let go ahead and add `margin: 10px;` and `border: 10px solid black;` to the padding class as well. Let's inspect that element in the browser and you can see Chrome's clear depiction of content, padding, border and margin.

All these different sizings can be confusing. This can especially be frustrating when you think something's 20 % when in actuality it isn't.  Enter box-sizing.

At the top of our `styles.css`:

```css
* {
  box-sizing: border-box;
}
```

Now when we refresh, all of our 20% widths are the same regardless of padding. It also includes border! However, it does not include the margin.

## CSS Properties and values
References

https://developer.mozilla.org/en-US/docs/Web/CSS/Reference
https://css-tricks.com


# HTML, CSS and Javascript (20min)
HTML (content), CSS (style) and Javascript (behavior) as the main components of front-end web development.
- Q: Sum up the roles HTML and CSS play on a website in a couple of sentences.
  - HTML: Structure
  - CSS: Styling
  - JS: ???

Exercise result categories
- Interactivity
  - Click something, something happens.
    - Like: increment Like counter.
    - Comment: submit comment, appended to post.
  - Javascript defines what happens on a page depending on how you interact with it.
- No Refreshes / User Experience
  - When I comment on a post, Facebook is able to process my new comment and render it on the page without refreshing the entire page.
  - Gives the page a much smoother user experience compared to a static page that doesn't have this sort of functionality.
- Communication with a server
  - Javascript is somehow telling a server that (a) a user has done something, (b) save that interaction and (c) display the results of that interaction to all other users.
- Not an exhaustive list of Javascript properties, but we'll go over these and more in more detail later on in the course.

So, to the main three components of front-end web development up in one word each...
- HTML: Structure
- CSS: Styling
- Javascript: Behavior
  
  # JS: Pega and JS
  
  Example:
  
  ENUMCB.Who_VLDN = function() {
    var isDKRefVisible = ENUMCB.getIsDKRefVisible();
    try {
      if (isDKRefVisible){
        var answer = pega.ui.ClientCache.find("pyWorkPage.Respondent.DoesKnowResident");
        ENUMCB.Required("pyWorkPage.Respondent.DoesKnowResident","pyWorkPage.Respondent.DKRefused.Who");
      } else {
        ENUMCB.Required("pyWorkPage.Respondent.DoesKnowResident");
      }
    } catch(e) {
        alert("***ENUMCB Error -" + e.message);

    }
};
  
  function EnumCB_Who_POST() {
  var workPage = pega.ui.ClientCache.find("pyWorkPage");
  ENUMCB.Who_VLDN();
  if(!workPage.hasMessages()) {
    var respPage = pega.ui.ClientCache.find("pyWorkPage.Respondent");
    var questFlags = pega.ui.ClientCache.find("pyWorkPage.QuestFlags");
    var answer = respPage.get("DoesKnowResident").getValue();
    if(answer == "yes") {
      questFlags.put("NextSurveyQuestion","PopCount_QSTN");
    } else {
      questFlags.put("NextSurveyQuestion","ExitPop_status_QSTN");
    }
  }
}

