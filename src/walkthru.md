## Referencing Angular Material Theme Colors for Styling
## With Bonus 'Altering Angular Material styling' Content

We are going to begin with a generated Angular Material Custom Theme.   This is all possible with a pre-built theme, but much more difficult because the css is already minified and you do not know the theme names.   

It should be noted that many AM stylings themselves do not work properly if your app is not properly configured for it.  This is covered in their theming guide but bears emphasizing:

Many Material styles are nonfunctional if the content is not either:

* Placed within a <mat-sidenav-container> element.
or
* You have not added class="mat-app-background" to the body element of your index.html (the same place they automatically add mat-typography).

These set the 'background' element for the light/dark theme background of your app, and dark themes in particular will break without it (as you get white text-on-white).

## Angular Material and SASS

Angular Materials' themes are generated using function-type features of SASS.   This all occurs in the custom theme file (usually your /app/styles.scss, though it can be in another file that is imported).   The SASS output is then -appended directly into the DOM in <style> tags in the <head> of index.html.    This is a big part of why Angular Material is so difficult to modify: because the css is injected directly into the DOM, it is always more recent than your component stylesheets and classes, and overwrites them by cascading principle.   

Similarly, the variables that refer to the theme colors only exist in the SASS file that defines and processes them.  Consequently, to either style your components in your theme colors (and have them respond if you change themes!) or to modify Material element styles, we must do the same thing: utilize SASS in the styles.scss file.

## A simple walkthrough

I have prepared a simple app with one component and a custom theme that is already generated.   We have two branches, one which shows you how AM -intends- for you to do this.    AM expects you are creating re-usable component pieces (like they do), and consequently will want to re-use these components throughout your application.   

I will then show you how to make simpler changes.   This is only really appropriate for smaller tweaks across your entire app.  It is also how we will demonstrate how to modify Angular Material's existing styling.

We will begin with the 'intended' route.   We have already completed a few steps along this route. 

* ~~Define your custom theme.
* ~~Create the component you intend to style and put classes on it to reference.
* Use Angular Material's Theming functions to define a theme mixin (essentially a function) for our custom component
* Import the component theme mixin to styles.scss
* Include the component theme, passing it the application theme as an argument.
* See results.

Our 'short and sweet' route also overlaps with modifying AM.  In this route, we do the above, but we do the work directly in the styles.scss file instead of creating a component styles file and importing it.   Because the output is calculated with styles.scss, our changes are the most recent and they can overwrite AM's styling (assuming equal or higher specificity, like any css.)

