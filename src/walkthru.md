## Referencing Angular Material Theme Colors for Styling
## With Bonus 'Altering Angular Material styling' Content

We are going to begin with a generated Angular Material Custom Theme.   This is all possible with a pre-built theme, but much more difficult because the css is already minified and you do not know the exact name of the theme variables.   

It should be noted that many AM stylings themselves do not work properly if your app is not properly configured for it.  This is covered in their theming guide but bears emphasizing:

Many Material styles will not function correctly if the content is not either:

* Placed within a \<mat-sidenav-container> element.

    or

* You have not added class="mat-app-background" to the body element of your index.html (the same place they automatically add mat-typography).

These set the 'background' element for the light/dark theme background of your app, and dark themes in particular will break without it (as you get white text-on-white).

## Angular Material and SASS

Angular Materials' themes are generated using function-type features of SASS, called mixins.   This all occurs in the custom theme file (usually your /app/styles.scss, though it can be in another file that is imported).   The SASS output is then -appended directly into the DOM in \<style> tags in the \<head> of index.html.    This is a big part of why Angular Material is so difficult to modify: because the css is injected directly into the DOM, it is always more recent than your component stylesheets and classes, and overwrites them by cascading principle.   

Similarly, the variables that refer to the theme colors only exist in the SASS file that defines and processes them.  Consequently, to either style your components in your theme colors (and have them respond if you change themes!) or to modify Material element styles, we must do the same thing: utilize SASS in the styles.scss file.

## A simple walkthrough

I have prepared a simple app with one component and a custom theme that is already generated.   We have two branches, one which shows you how AM -intends- for you to do this.    AM expects you are creating re-usable component pieces (like they do), and consequently will want to re-use these components throughout your application.   

I will then show you how to make simpler changes.   This is only really appropriate for smaller tweaks across your entire app.  It is also how we will demonstrate how to modify Angular Material's existing styling.

We will begin with the 'intended' route.   We have already completed a few steps along this route. 

* Complete: Define your custom theme.
* Complete: Create the component you intend to style and put classes on it to reference.
* Use Angular Material's Theming functions to define a theme mixin (essentially a function) for our custom component
* Import the component theme mixin to styles.scss
* Include the component theme, passing it the application theme as an argument.
* See results.

Our 'short and sweet' route also overlaps with modifying AM.  In this route, we do the above, but we do the work directly in the styles.scss file instead of creating a component styles file and importing it.   Because the output is calculated with styles.scss, our changes are the most recent and they can overwrite AM's styling (assuming equal or higher specificity, like any css.)

This is very similar to how you create an alternate theme: You define the theme and then @include it under a class that you can apply to apply the alternate theming.  In this case, however, the @mixin creates a theme with variables based on the theme name you give it; you could also have the mixin modify those colors for a darker/lighter shade (mat-color:($accent, A400), for example).  This is also how you retrive other parts of the palette (such as text colors). Many Angular Material components automatically utilize variations of the core theme colors.   You can visit the Material Design website (Material.io, not Angular Material) where they have a palette tool that allows you to input a color and see it's darker and lighter shades.

Lastly, there is one classification of Material components that are particularly difficult to style and modify.   All overlay/modal components of Material, and their cdk core components (such as snackbar, dialogue, select menus, bottom sheets, etc) live in a special overlay container that is created by Material and placed into the DOM outside of every component: it is added to the \<body> outside of your base app-component file.   This means you can't easily add classes to these elements (You would have to do so with a conventional JS getElement / classList.add after the website has already been rendered). 