# Build View

Coming soon...

Our autocomplete thing works nice on you had a page, uh, but it actually doesn't work
at all on the article. New Page. So if I go to `/admin/article` and click creates,
there is nothing here. Okay. It looks like it's working, but that's actually just the
normal autocomplete coming from my browser, not actually my magic. And there's no
JavaScript error. It's just that

we haven't added the JavaScript for this page. So we have the class on there, we have
the data complete, but remembering edit that age Montsweag, that's where we included
the JavaScript and the style sheets that uh, that rented us. So unfortunately there's
no like really clean way to automatically include some JavaScript or css on your page
when you are using a specific field, but something that you need to think about. So
we need to actually copy all of this JavaScript and css stuff and then down in our
`templates/article_admin/new.html.twig`, we need to make sure that that stuff
is actually there. And like I mentioned earlier, we're in a little while. We're
actually going to change this so that the author field is only filled in on create
and then it's going to be disabled on edit. So once you set the author, it's going to
be set for good. So we actually, we don't really need any of this stuff on the edit
page. I'm actually going to delete it now if you do need it, some css and JavaScript
on both your edit template and your new template and you don't like that duplication,
I don't think it's a huge deal, but if you want to, you could create a new base
layout, a new layout file called like

`article_admin_base.html.twig`. It would extend `content_base`, but it would
override a, that's where you could add override those, uh, of those blocks, those
blocks. Then your children template would extend this new template that you're just
using a for your article Admin area. So there is a way to remove that duplication if
it bothers you. But now that we've moved the CSS and the gas over

Nice, now we get our proper out of completion. Cool. So there's one other cool thing
I want to show you and it's sort of a minor problem that we have right now. Close a
few of these templates will closed a few of these files and go into my `UserSelectTextType`. 
Right now the whole system works because we are setting a default `attr`
option and we're sitting in the `class` and `data-autocomplete` you were attributes. Open
up your `ArticleFormType` where we use this. One of the things that we're allowed to
do is we're allowed to set override that `attr` theory. If we wanted to promise if we
did that, this `attr`, our option would completely replace this `attr` year option here.
And we would lose all of these special aid ctr things. Not the biggest deal ever, but
we can do things in a little bit of a better way. Uh, go to the bottom of your 
`UserSelectTextType`, go to the code, generate menu or command n on a Mac Pitt override
methods in select `buildView()`. Notice there's also a method called `finishedView()`. The
purpose of that is almost identical to `buildView()`. Alright, so here's the deal,
whenever Symfony renders your form,

it creates a bunch of variables that are used to render that to Brenda, that field.
We already know this in `register.html.twig`, we were actually overriding
these `attr` variables and in our `form_theme` template, we were actually using a
different variables inside of here. Another way to look at this is once again on your
profiler for your form. Every field has a bunch of view variables that power
everything about how that field is render someone Symfony

in order to get those variables. Symfony calls the `buildView()` method on every single
one of your fields, and that's our opportunity to add or change whenever variables we
want. We do that with this `$view` variable, which is kind of a strange variable. So
check this out. `$attr = $view->vars['attr'];`. So this `$view` object has a public `->vars`
property which is a little bit strange and everything on that vars property is
eventually going to become a variable that's available in your template. So if you
want to change the atr variable, you do it by changing that key on that property. So
here, let's now say `$class` equals, we'll do a little `isset()`, we'll check to see if
there already is a class a view variable,

um,

because if maybe somebody set the `attr` option, which becomes this view variable, I
need to explain that, then we'll use `$attr['class']`, but we'll add a little space on the
end of it or else we'll just set it to an empty `string`. And then we'll set the `$class`
two `js-user-autocomplete`, same class I've had been using above. Then I'll set this
back onto the array. And then we also want to do the `data-autocomplete-url`. So
actually copy that from above. Will say `$attr['data-autocomplete-url']`, and then
I'll clean that up, turn that into an = a semicolon on the end. Perfect. And finally,
we'll set this many to set this back on the, uh, the view objects that will say
`$view->vars['attr'] = $attr;`. So previously, by setting the `attr` option internally, Symfony
always converge that into an att are variable. Now we don't need to set the option,
we're just going to make sure that regardless of whether or not the user set the
eighth year option, we're going to properly make sure that the stuff that we need on
it is set as view variables. So with any luck,

we should be able to go over refresh and yes, everything still works perfectly
because all of the same class and auto you were out, things are being added on there
properly. And if you open the profiler for our form, we can actually see this. It's
kind of cool if you click on author and go down to view variables, you're going to
see that the aptr variable actually has these values. So these are what's being used
and are vendors that. All right next, let's do something else.