# Custom Field Theme

Coming soon...

The last thing we need to do is fix this, agree to terms box. It doesn't look that
bad, but you know this markup is not the market that we had before, so let's fix this
to do this. This is actually interesting. We basically want to override override how
they form row is rendering, but just for this one field and we can actually do that.
Go back and open the web debug toolbar for the `Form` system.

Then click on the `agreeTerms` box and go down to the view variables. Few minutes ago
we looked at this `block_prefixes`. Remember what happens is if you, whenever you
render each, when you render each part of the form, it's going to look for a block
that starts first with `_user_registration_form_agreeTerms` like 
`_user_registration_form_agreedTerms_row`. If it doesn't find that, which of course 
it doesn't, it then looks for a `checkbox_row()`, and if it doesn't find that it uses 
`form_row()`, which is what's happening in this case, and so ultimately it is of course 
using the same block `form_row()` as everybody else. But if we want to customize just 
hubby row of this one field is done, we'll copy that long block name and will override 
`{% block _user_registration_form_agreeTerms_row %}` and will say `{% end_block %}`. And 
inside here I'm just going to literally copy and paste the old field.

Boom.

It's not perfect yet, but when I go back, find my terminal, find my main tab and
refresh. Oh again, an error at temple that extends another one. CanNot include
content outside of toy blocks because I put, pasted that in the wrong spot and paste
that in the right spot. Come back, refresh. And yeah, so you can see it moved over
just a little bit

and is using our new kind of simpler checkbox `mb-3` label setup. So the cool thing is
is that yeah, this, this is nice, but you know, if there's a validation error, it's
not going to show up. We're just rendering everything manually. So what you want to
do is you want to make sure that you take advantage of as many of these variables as
you need to in order to make this really rendered the way you want to. So first thing
I'm gonna do is I am going inside of here, we're gonna call `{{ form_errors(form) }}` 
to make sure that my validation errors show up. I can also call form_health forum if I wanted
to, but since I'm not adding any help text this field, I don't need to. Second thing
is this `name="_terms"` that actually is a problem because the form is expecting to
be called a certain way and if it's not called, it has a different name. It's not
going to process correctly. Fortunately, one of the variables we have access to his
`full_name`, so we going to say `{{ full_name }}` and that's it. Yes, we can get
fancier. We can use the `ID` attribute if we want to set the `ID` properly, if we care,
it's all up to how far you want to do things.

You can look through this and get as fancy as you want to. You can also use the `errors`
is variable here to check to see if the ehrs are not empty and you could, for
example, add a special errors class up here. Something like `errors is not empty`. Then
we print some special class. That's up to you. Point is get as fancy as you need to
for your actual situation. It's now recover. Refresh this. It looks good and it's
also going to play nice with our system because it has the proper input type.