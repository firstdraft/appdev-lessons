# AD2 Helper Methods Pt 2

**BENP: Document based on descript transcription of AD2 WS 2023 Helper Methods Part 2 Video.**

## Welcome back

**Raghu:** [00:00:00] Welcome back. Hopefully all of your anchor elements are now nice linked to helper methods instead. And it's time now to work on our forms and turn those into helper methods also. And this is gonna pay big dividends for us down the line. So let's start on that process and I'm gonna pull up my workspace again.

Head over to our new form in app movies, app views, movies. New. [00:00:30] Here we have our form element. And let's look at the new helper method that's gonna help us write these tag opening tags. It's called form width and it needs some arguments and specifically it needs a hash that's gonna tell us the action. So I'm gonna say movies path just like below.

And then. I'm gonna give it a [00:01:00] block. And the reason it needs a block is that it needs a closing tag. So many of our view helper methods that output html, like HTML elements, are gonna require an end, a closing tag. So that's what this is gonna, we're gonna create closing tags by providing a block to the method, and then put the end of the block where we want the closing tag of whatever opening tag this method is gonna create for us.[00:01:30] 

So if I do this, let's take a look at what this produces, and as usual, I'm gonna view source and see. So here's what we wrote by hand. This is what the output of that helper method was. So it's a form action equals movies and it actually does, uh, more stuff than we were doing by hand. And these are all good things that we should have been doing by hand.

It sets the default except character set for the form. Look at this, the [00:02:00] form with helper, right? So just this and nothing else automatically created this authenticity token for us that we had to do by hand. And we learned about how to do that. But actually, once you start going down the path of using the form with helper, you don't have to manually worry about putting in this CSR f authenticity token.

Fantastic. So we can go back to app dev one mode where we didn't have to think about this. [00:02:30] Excellent. All right, so that takes care of our opening tag and our authenticity token. Now I can basically get rid of this and this, and I can move all of my inputs inside this helper method, and we now have a better.

Form [00:03:00] opening tag and closing tag being created by the helper method. And then all of our other H M L just goes right inside. Great. Now what else can we do? Well for divs, there's not really much we do for labels. There is, we can do a label tag element and then we provide copy like this. Let me take a look at what ha that [00:03:30] outputs.

Take a look at the source code. So here's what we wrote by hand. Here's what that helper method outputted. So if we just say title, it's gonna use that for both the copy and for the four attribute. But if we want it something different for each of these two. Then we need to provide a second argument here.

Title box. The first argument is the four attribute. The second argument is gonna become the content [00:04:00] because in some sense, the first argument is more important. It's the four attribute. And then the second argument is the content for that element. So that is label, and now we can get rid of this. Great.

And then we also have helper methods for our inputs. And you might expect it to be input tag if we're following the same kind of pattern, but it's actually not because we have a separate [00:04:30] helper method for each. Of input. So we have a text field tag, we have a number tag, we have a checkbox tag, we have a text area tag.

So we have all these different helper methods that output different types of inputs. But then we have as an argument, I'm gonna say query title and let's just start with that and see what it outputs here. The output of the method is this input type text, cuz it's [00:05:00] the text field tag. And both name and ID are both query title cuz I only gave it one argument of query title.

So it's pretty close to what we have written by hand before, except that we want a different ID for it. So I'm gonna have to provide more arguments. Now the second argument to this method, the first argument is assumed to be the name and if you, and then it's gonna use that for the id. Two second argument is gonna [00:05:30] be the.

The value attribute. So if you want to prepopulate the input, the second argument is what will be used. So if we take a look at this, whatever is in that second spot will be used to populate a value attribute. Okay? So that's good. That'll be handy for us. In fact, what we're gonna want to do is prepopulate prepopulated with this.

That's what we want in that second spot in case. So this is for when validations fail and if we're re-entering the page with error [00:06:00] messages, we wanna put that in there. So like in this situation, um, oh, I didn't actually add, I have no validations. I thought I had one. Let me do title presence. True. So now we can go back

and

some syntax error.[00:06:30] 

Okay, so, okay, so here's my now two inputs and in case of validation error, the title can't be blank. Let me type in some description here, [00:07:00] and if there's a validation error, we render this and we're getting this message here. Let me add another validation just for kicks and say description should also be present.

Now if I say this is blank, some title create says description can be blank, title can't be blank. Let me say some title [00:07:30] in both of these boxes. And this is working just like before because we're populating it well using the second argument here. Okay, great. And after that I can pass a hash of any other options that I want.

Zebra, giraffe. And this will then become arbitrary H T M L attributes on [00:08:00] the element. And this is true of most of our helper methods that output a string of H T M L. If you just need to put arbitrary H M L attributes, you can pass a hash as this last argument. In our case, what we wanted to customize the ID and make it something that is not conventional, conventionally, we use actually just title for everything.

And that would be the name. That would be the id. It would be the same for all of them, but if you want them to be different like this, then you can just pass it [00:08:30] as that last hash of arbitrary whatever attributes you need to put on that element. Great. So now we can do everything that we could do before, and it's actually a lot better.

So I'm gonna delete this old one and we are in great shape. We'll do the same thing for description, label, tag, description, description. Oh, this should be [00:09:00] description box so that that populates the four attribute. And then I'm gonna do a, in this case, it's a text field tag,

no text area tag. And then this one, the name should be query description and we should pre-populate it with this [00:09:30] description if it exists. And then we want an ID on it of description box so that the app, so that the label matches properly with it. Okay, great. And also, I said that I was gonna stop using these, so I'll stop using these and we'll be very terse, [00:10:00] even though it's not my favorite style.

And if we examine the text area that was written. Here's this one. Here's this one. Oh, this one had rose on it. I. When we wrote it by hand, we put rows on it. That's okay. Like I said, we can put an arbitrary, any pairs of HTML attributes that we want in there. And so we got that. We got with that, we got that.

We've achieved parody and I'm gonna delete [00:10:30] the old raw HTML versions. One more time. Let's just give this a whirl. Add a new movie. Try this one, try that, try this, try this. Great. Everything looks good. And the last thing is this button. And even for this, we have a button tag[00:11:00] 

create movie. And that's about as simple as it gets. It's just gonna put that button in for us. And we're good to go. All right, so now we've replaced all of the essential parts of this form other than just divs that we use to organize it with helper methods. Ultimately, the output is the exact same H T M L as we had before, but [00:11:30] it's better in many ways.

The most concrete way in this example is we didn't have to generate the cross-site request for a re token manually. That's gonna save us a lot of work over the hundreds of forms that we were gonna make. We don't have to worry about creating the hidden input and populating it with the form authenticity.

Token derails, just by default, almost invisibly now takes care of that for us. Fantastic. Alright, and we're gonna do the same update. I'm gonna copy this. [00:12:00] We're gonna do pretty much the same update for our edit form and. The edit form. I'm gonna paste this here and it's pretty similar. The difference is I'm gonna, actually, before I do this, what should I do?

I should make a gig commit. So let me get this going. You might notice that this Web Git client is slower, and that's because we're using [00:12:30] Vanilla Rails, which uses a different asset management system that's a little bit more complicated, doesn't play well with our Git gem. The good news is that we're not gonna be using this Git interface for long, cuz you all are gonna learn command line git, which is what most developers use.

So maybe just one more project we have to use this for. All right, so replaced new form with form with. Now let's do the same for our edit form. And first we'll do the opening tag [00:13:00] form with. URL goes to something and we'll have our due, then we'll have our end.

Now what do we put here? Well, we can just start to move it over bit by bit from the handwritten version. We don't have to specify method post because the form width uses that by default. If you [00:13:30] wanted to do a method get, then you would have to specify that. It's basically the inverse of H T M L H T M L element.

The default method for a form is a get, but rails knows that most of our forms should post. So it flips the default behavior. Okay. I don't have to do the authenticity token. I wanted this method to be a patch. Okay, great. So now I can take advantage of this and do method patch, [00:14:00] and it will also automatically generate this.

Here. So let's take a look at that. Before I delete everything, let me put this back. Actually we can compare the two put method. Get here, there's patch. Rather take a look at the output of this

show details. Go to an edit forum, view source resource. And now here's [00:14:30] our new form width output and you can see that it put in the right action compared to the previous one. I copy pasted this out, but it used to, it added the car set, which is good. It used the method post like this one did it automatically put in the authenticity token kitt, which is good.

And it automatically generated the method patch. So both of these hidden inputs that we wrote by hand we can get rid of. Awesome. [00:15:00] And we put in all the contents for our stuff inside. But if you think about the content for our stuff, label for title with the value of the movie title, description, value, description.

The only thing that's different between the create form and the update form is the copy on this button. So I'm gonna delete all of this. Go to my new form. I'm just gonna copy this, just paste it in cuz [00:15:30] now all this is the same, assuming that this instance variable is the same, which we did name it the same.

So we got lucky there. But then I just sort of update this copy of this button and then it should be good to go. Let's go back. I'm gonna go back. Let's edit something that has something in it. Edit, update. Looks like it works. Fantastic. Okay, so now we have a much better. [00:16:00] Update form using the form with helper, which again just writes HTML for us, but now it saved us two things.

The hidden input for the authenticity token and the hidden input for the method patch. Excellent. Okay. Now what should we do next? Well, I'd like to spend some time refactoring our controller. Our views are looking great. Our views, we are much more concise. We're using Ruby Helper methods embedded in the view templates to generate H T M L in a more secure way and in a [00:16:30] more reusable way using route helper methods.

Let's spend some time in our controller. So right now there's a few things we need to improve. There's some hash literals and we can do a lot of work with those. So like anywhere we have the explicit curlies, we can, we said we were gonna get rid of these and so we should. [00:17:00] And, oops, that's not great first.

Okay, next. We also said we're gonna use the new hash syntax, so we should do this wherever we can. Okay, so that's better. Alright, uh, and here to create that, this is when the new [00:17:30] hash syntax starts to bother me is when you have symbols for both the keys and the values. It starts to get a little confusing, but just remember to unwind it in your head to the old syntax.

All right. Now in APT Dev one, we wanted to be very clear. A lot of students tended to get confused about getting a collection of records. And that was an instance of the class active record relation. And then [00:18:00] you have to then go an extra step to take the first record out when you're working with only one record.

For some reason, when we didn't do this three step process for, for, for years, we didn't do this three step process, students would get very confused between an active record relation, which is a collection of multiple records, and then one instance of active record, which is just one [00:18:30] row. So we like were we, were very deliberate about always doing it in three steps.

First you get the id, then you get a record. Then you get the set of movies that are all matching this Id. Even though we know it's unique and there's only one, then we get the first element out of that array, which is the object that we're looking for. Now, as you might expect, professional rails, developers do not do this.

First of all, this typically is done in one line. [00:19:00] We, this is a spot, a place where pip, usually people don't even, I usually don't make an intermediate variable for that. And you know how much I love my intermediate variables. So usually it looks more like this, but even then this dot where, and then dot first can typically be done on one line, so that you just have this.

And if [00:19:30] you're gonna do that, then there's a method that is designed to do exactly that. It's called Find by, and it's exactly the same thing as dot wear. It's just that it goes and finds all the matches. And regardless of how many matches there are, it just takes the first record out of the set of matches and returns that first.

Record to you. So it'll either be one record or it'll be nil. So if we pop open a [00:20:00] rails console and give this a shot and side note to open new terminals, now I have to go over to my little plus here in the VS code interface. But if I open a Rails console and then I do movie dot find by

ID one, I get nil. Let's look at Movie dot. All right. [00:20:30] Now first ID is three, that's why. So I do movie dot find by ID three, and it just gives me back the individual instance, not an array containing it. And I can just go ahead and say title right away. So that is how the fine by Method works. And. Even better than that.

There's another method. Instead of find buy, this is called find, [00:21:00] and this only takes an integer and the find method assumes that you are searching by ID only, you can't use find with any other column. You're, you're definitely, you must be looking in the primary key column. In that case, it's gonna do the same thing.

The difference in behavior is if you provide an ID number that doesn't exist, it doesn't return nil, it throws an exception of class. Active record. Record not found. And this [00:21:30] is really handy to have an exception thrown sometimes when you don't want the code to proceed any further. If somebody tries to access a ID number that doesn't exist and you wanna stop with an exception and in a Real Rails app, let's show you what happens here.

I'm gonna switch this to just a find by prams of ID and comment this out. Now I'm gonna go to [00:22:00] movies slash six works just like before, if I go to movies slash something like this, now I get this active record record not found in. Once I push this to Roku, and once this is running in production mode, this error message shows up as a 4 0 4 page, which is the correct behavior.

It doesn't show up as a, something went wrong, 500. It doesn't report an error to us. It just means that somebody tries to navigate to a resource that doesn't exist, stops the action, doesn't proceed any [00:22:30] further, and just returns the 4 0 4 page. So this is a special type of method. It returns an expected type of exception when it's given an argument that it's not expecting.

Alright, so from now on, This is what we're gonna do in all of these actions that are looking up a, an individual record based on an ID number. We're just gonna do [00:23:00] movie dot finds, dot fetch id. This is the right way to do this.

All right? And another thing is, just so you're aware, conventionally rails developers don't say the underscore movie. I [00:23:30] did that in app dev one cuz I wanted to be very explicit that I was just making up whatever variable names that I wanted in actual rails applications. The convention is name these variables the same thing as the class name and the controller name.

I reason I didn't do it in Apt Dev one is because people seem to think that it had to match the model name, but it doesn't have to match. You can name one of your variables, whatever you want to, but you know it's just a convention and you don't have to like think about [00:24:00] what to name it. Just name it. The same thing as the model.

As long as we all know now we're on the same page. We make up whatever variable names we want to. So similarly list of movies conventionally, they just call it at movies, and I'm gonna make this all more concise as well. Movie dot order render JSON movies. This is starting to look like a professionally written rails controller.

[00:24:30] Now the only thing that doesn't is these inputs where we did query underscore back when we were learning that these things come from. The names of our inputs, which go into the query string, which then go into the pram slash, which is what we're fetching out of. So we use this prefix to remind ourselves of that.

I am now going to get rid of it [00:25:00] and just use the name of the column, which is conventional. And again, the reason we didn't do that before is people seem to think that this has to match with this, but no, it doesn't. What this has to match with is whatever we name our inputs, that's what it has to match with because that's what's going into the pram.

Sash, which is what, what we're fetching out of. So that's all that really matters. So I'm going to get rid of [00:25:30] this while we're on the topic. This underscore box, for the same reason, this suffix doesn't really exist in conventional code base. People understand what the difference is between four and ID and name and value.

And so the, they don't need to name them separately to help them keep them straight in their minds. So it's like less mental cognitive overhead to just name everything the same thing. So that's what you'll see in professional code bases, which [00:26:00] then allows us to not have to specify them separately here, cuz it'll use this first argument for everything.

And even here, if you do it like this, it's just gonna capitalize this and use it for the content. So Rails will be pretty smart. You can just say label tag and it'll use it. Title it'll call dot Title Lies on this to actually draw the form. So let's go here. Nope, I broke my edit form because this variable doesn't exist anymore.

So the index [00:26:30] page can't be accessed. So I have to change this to at movies while I'm here. I'm gonna change this to just movie, which is the conventional block. Typically, the array is plural. The block name variables, typically the singular version. Now again, you don't have to do this if you don't want to.

If you like the very long descriptive variable names, feel free to keep those for as long as you want to. But I just wanna show you what a conventional code base is gonna look like when you get [00:27:00] out into the world. So now my index page should work again. Now if I go to add a new movie, this, the movie variable doesn't exist.

Again. Go back to new at the movie. Everywhere is just movie now. And now this form works. Notice that this was properly, these both are properly capitalized, even though, oh, lemme get these out of here.[00:27:30] 

These out of here,

don't need this anymore. Don't need this anymore.

And these labels are still fine because Rails is smart enough when it's creating the content of the label to capitalize are actually title [00:28:00] this. And so that's why we can just say label ti title and it and it does both the four attribute and the content properly cuz it capitalizes. All right, looking good.

Look at how much shorter and shorter and shorter our code is getting as long as we start to follow conventions. And you ain't seen nothing yet.

Okay, looking great [00:28:30] show. Ah-ha. This one I still haven't updated to at movie movies. Path. Looking good. Let's make sure that still works. Looks good. Find method errors. Forgot to change this instance variable in the edit page.

All right. [00:29:00] And in the edit action. I didn't change this variable,

I'm just making this all the same. Everywhere again. In Apt Dev one, we named things differently. We named them differently in each action to make sure people understood that. Each action is completely independent and had nothing to do with any other action. So we on purpose named our variables different in everyone.

Now that we understand that we're gonna do what's convention, which is just name the [00:29:30] variable movie in all of these actions, and we don't have to think about making up different names in every action. All right, looking good.

That was a lot of refactoring. Let's make a get commit. And what else can we approve about this controller? It's looking really good. So far. One thing is in the prams hash. [00:30:00] Typically we use symbols and knot strings, so we'll follow that convention and be consistent about it.

You can use them interchangeably only in the prams hash, nowhere else. Most hashes, you can't just interchangeably use strings and symbols, but the special rails, hashes of prams and a couple of others, you can. Um, that looks good. [00:30:30] All right. This is looking great. Lemme make one more commit here. Refactor.

Lets say modernized controller. All right. Now there's one major topic left to talk about, and that is the following. I can, in my [00:31:00] forms, I'm gonna demonstrate this with a form, like a plain old HTML form. And I'm gonna say just form for now. I'm gonna have a button to submit this form, and so we're gonna keep it as simple as we can.

I'm gonna have an input, I'm gonna have a name, and let's just say Zebra. Start with, and this was my new impact. I'm [00:31:30] gonna move this to my index page. Let's put it right here at the very top so it's easier to find and just show you, here's that input. Oh, I didn't close my button.

So this entire page is not my button. That's kind of cool. All right. So I say hi and let me close. Get my server log here [00:32:00] and then submit, and we'll see what happens here. Zebra. Hi. Okay, I'm gonna move this over to the left. And move this over to the right. Should make it a little bit quicker to jump back and forth.

Close the sidebar. Okay, so we got our prams zebra high as expected right now let me show you something kind of [00:32:30] cool. I can do zebra and put some square brackets next to it and let's just see what happens With only that one change, I'm gonna now say hi again. Clear my server. Submit. Now take a look at how this worked.

It put, it still had a key of zebra just like before, but instead of putting high as the key, it created an array [00:33:00] and it put high as an element of the array. So that's interesting. Ha. And let me put in another one of these. I'm gonna put another input in and let's refresh. I'm gonna say hi there, and then I'm gonna clear my server log and then submit.

And now look what it did. [00:33:30] Both inputs have the same name and rails. If we follow this convention, this is a rails thing. Rails. If it sees this weirdness of two names, but it happens to end with the square brackets, it understands that what we're trying to achieve is we're trying to capture both of those values and put them under the same key in the prams hash, but put those values in an array.

So now I can do a prams dot fetch of zebra, and I can have an array of however many of [00:34:00] these are, and I can do a dot each. And. Maybe create a list of tags or something. So what this is very commonly used for is input type checkbox. And you have something like this. You might have some labels in here except, or let's say red say value [00:34:30] equals red label blue

and value equals blue. Now I'm gonna submit these, just let's just check one to start command K to clear submit. Now you can see that only red was checked and that was the only value that went in if I checked both. [00:35:00] Now both of them go into this. So this is how this kind of naming convention is how you can create nested structures within your prams hash.

Interesting, interesting. So let's look at this a little bit more. This gives you a lot of different power and flexibility. So this is a very common use case. It, it's like basically you can draw a list of tags and let people check them off and then [00:35:30] submit, and then you get an array and you loop through the array and then you can create a join between each of those tags and whatever record the per the, the user is creating.

What else? Well, other than the classic many to many checkbox situation, I go back to type text and I wanna do something else I'm gonna do, we'll just leave those values in there to save me some typing. But they're type text [00:36:00] now. Watch if I do giraffe, what if I put a value in there? Now what's gonna happen?

So I now have this form. Zebra, zebra. I put the square brackets, but now I put something else inside the square brackets and I type in some stuff. 1, 2, 3, 4, 5, 6. Imagine I just typed in some values. What do you think the peram hash is gonna look like? Now, take [00:36:30] a guess. Is it gonna be an array again with values, giraffe and elephant in it?

If so, what? It's gonna happen to red one, two, and three blue. Where is this food gonna go? Is it gonna be nested arrays? Two levels deep. So the key will be the top level key will be zebra and the peram slash then the value will be an array. Is it an array of arrays? Let's, let's see. [00:37:00] So as, as always, top level key in the prams hash, we got zebra, but now the value is a hash, so nested hash.

And the first key for this input is giraffe, and it's got a value of whatever I typed. The second key is elephant, and it's got a value of what I write typed. So this is a very handy way of bundling [00:37:30] together related inputs in a form into a subhash. So they're not all in an array. They're labeled in a subhash, which is really handy as well.

And this is actually the technique that we use more often. The first technique I showed you is useful mainly for check boxes, which are not that common, but this is super common. In fact, this is the technique we use for 95% of our forms is. All of the inputs that are [00:38:00] related to one model type object, a movie or a director, anything related to one database record.

We want to bundle them all together into one subha and store them in a key movie or director or event or whatever. We want that to be a top level key in the pram slash and then the subhash should ha have all of the attributes for that top level key in that way if we want to. It's very easy to have attributes for multiple different objects [00:38:30] in the same form if we need to.

Alright, so let's re, given this principle, I want to reorganize our form a little bit. So I'm gonna go back here. I'm gonna bring this back here. And given this, I want to think about our new form and what I wanna do. Is put all of these [00:39:00] into a, in the prams hash. I want them all to be in a subha under a key called movie.

So what I'm saying here is I want the prams hash to end up looking like movie. And then I want title, some whatever I type. And then description.

This is, this is my goal. I want the prams hash [00:39:30] to look like this. So I need to name my inputs in, in a particular way. Okay, cool, cool, cool. That means, so this is, what is the name of the inputs? So I'm, I had 'em a very concise form here. Now I have to make it like less concise, but that's cool. I'm gonna do, I'm gonna use strings here, cuz now you have to use those square brackets.

And I'm not sure if I can use square brackets and symbols, but, If I want the top level key, that means they have [00:40:00] to say movie and then title and movie, and then the description, and we'll worry about these labels in later on. We'll get all that to match up the labels and the IDs and the forests. We'll get that all tidied up later.

Let's just get this to work first. So I'm gonna go check out my form, view source, [00:40:30] see if this did what I wanted. So the input now has a name movie, Squareback title movie, Squareback description. So I think this is gonna do what I want when I submit this form, say sum title, some description. Of course, my controller actions are now gonna have to be updated, so I'm getting a missing parameter error.

But in the server log, [00:41:00] I got what I wanted in terms of the structure. I have a top level key movie and all of the movie related attributes, which could be like 30 of them, are nicely bundled into the subhash. Excellent. Now let's update our controller code to take advantage of this in the create action. I have to, well, it's gonna be a little bit more verbose now because I'm gonna do prams [00:41:30] fetch first.

I'm gonna fetch the key of movie. Then I'm gonna fetch, oops, I did thought I had multiple controllers here. Multiple cursors rather. So first I'm gonna fetch the Kiev movie, and then I'm gonna fetch. The next key, right? So you have to go two levels in. Okay, now this should work. And there we go. We're back to [00:42:00] having it work Like before now, you might be like, oh, wow, you just made extra work for yourself.

But trust me, we're, we're getting, we're getting there slowly, step by step. Okay? Here's another thing to realize. Let me make a good commit. So far, so good.

In my rails console, I want to look at a nice [00:42:30] technique. Let me just make this commit before I mess anything up. New movie form. Now, Nasts movie attributes subha within prams.

Here is what we usually do when we want to create a new movie. Movie can movie our new M title equals high M description equals bye m save. [00:43:00] Right. Great. There's a slightly more concise way of doing this sort of suppose you happen to have a hash laying around that happens to have keys in it

that exactly match your column names. Exactly right. So the hash has exactly the [00:43:30] same column names as the movie table. Well, I can say movie.new and I can give the new method, the hash as an argument. and the new method will iterate through the key value pairs and it will assign this value to the column that has this name and this value to the column that has this name.

So that just like that X is initialized with those values. [00:44:00] Mm-hmm. , maybe you can see where I'm going with this now. Right?

Uh, look at that hash and then look at the hash that came into our server log. I already cleared it, but perms fetch. So like the movie attributes are in a subhash [00:44:30] called movie, which means I can just pass them as an argument. to.new and imagine in your head if there was 30 of those. So there, there was in, in APTA one code, there's 30 lines of code of of assignments here happening every single time, right?

We don't have to do that. This is called mass assignment. the.new method is capable of receiving a hash containing all of the attribute value [00:45:00] pairs and it'll mass assign them to all of the columns for us.

Is this gonna work? Unfortunately, it's not gonna work. It's not that easy. My friends, if I say Alice, Bob and I create, I get this forbidden attributes error. What is this? This is Rails doing more fancy pants security on our behalf without us even realizing it. [00:45:30] This is protecting us against another type of attack, not a CSR attack, but a different type of attack.

Where if people know Rails does this and people know that Rails developers are blindly passing whatever parameters are in the form there, there's an attack where people manipulate the form, which already has that C S R F authenticity token in it. So they're gonna, in Chrome, they're gonna inspect the form that already has the [00:46:00] authenticity token.

Then they manipulate what inputs are in there to put inputs that are not supposed to be in there, and they'll modify columns that are not supposed to be modified like admin, and they'll switch it to true. So what you have to do is you have to say which attributes are allowed to be mass assigned like this.

You have to whitelist which columns you, you allow to be assigned in this manner. Because there are sneaky users. And that funny, it [00:46:30] was funny because the, the security researcher who discovered this hack, and we don't know how many times the hack was abused before this, but the person who publicized this hack, the way that he got attention, he, he's, he claims he reported it, but it, he didn't get enough attention from the Rails team.

So he hacked GitHub, made himself uh, an admin on the Rails repository, and then he made a commit to Rails itself. And then that got David's attention and then they made this change. So, [00:47:00] alright, we, what we need to do here is we say prams dot require instead of fetch and prams because prams isn't actually just a plain hash, peram is a very complicated and powerful other class.

It has a method called Require, which returns an object of another class, which has a method called Permit. Then you list, which, Attributes you will allow through for mass [00:47:30] assignment. So now if I try this, I noticed that I didn't allow description through, I only allowed title through. So description ran into that wall, title, got through, description, didn't, and now we get this red error in the server log.

That's really easy to spot. This is a super common thing. Whenever you add a new column, whenever I add a new column, I always forget that. I also have to whitelist it in my, what's called [00:48:00] strong parameters list. And then I look at my server log and I see this error message. I'm like, have strong parameters.

I forgot about the GitHub hack. And then I have to go in here and I have to do this. And then it'll work,

create, and now it works. Yay. Okay, so this is awesome. Oh my gosh, this my friends is the biggest code savings of all. Think about. How many columns we usually have in all of our, in our tables, usually not just two. And [00:48:30] then for, we have one of these, we have like huge chunks of code for all of these assignments in all of our controllers.

All of that goes away now with this mass assignment technique. So amazing. We can do the same thing. Uh, for update. I'm gonna allow you to do the update action yourself, but let me make this even more concise. Let me make this a, let me get, commit this first. [00:49:00] Now, one last thing

for this video. This is looking great. Love this. This is looking awesome, this form. This is the, this is the only thing that, and we have to make the IDs match up, and that's the thing that we have to do. Like I feel like I went a little bit backwards here. It was [00:49:30] nice, and then I made it less nice and it's gonna get even less nice once I fix these label tags to match up.

And then I have to add the ID back over here to both of these things, so I may, there's a better way here if we want this nested behavior. Essentially what's happening is when you're making forms, generally this is the right technique. When you're making a sign-in form or when you're making a search form, this is what you have to [00:50:00] do form with url label tag, text field tag.

These are the helper methods that you use when you're making a form for the specific purpose of creating a record in your database table using an active record instance or updating a record. That's a very specific job and there's a, a more specific method for that, and that will save us even more code.

It's actually the same [00:50:30] method. It's just a different way of using the method. It used to be a different method, but then they unified the two methods in rail six. So we're gonna use that. And as you know, most of what our applications do is crud. So actually 99% of our forms, the purpose of them is to just create or update one record.

So it's really handy that there's this other way of using it. Here's how it works. Instead of saying form with url, you say form with model. [00:51:00] And the argument for this now should be the object that itself, that you're trying to build a form for. Now, what the heck is this object? Oh, this was, remember, think.

Remember how we created a new movie Object. in the new action. Now we did that only because we were gonna draw this errors collection and if we did this and we didn't have any object there on the very first time somebody visited slash new before they even filled anything out, so there was no [00:51:30] errors, we would get a undefined method errors for nil.

So we're like, okay, we're just gonna create a blank object just to satisfy that so that when we re-render the page later from a different action, we can use the reuse the same template. So this object will have an errors collection in this case, and it allowed us to be lazy and reuse the same template from two different actions instead of creating two different templates that have 99% of the same code.

But hey, it's gonna come in handy for us [00:52:00] that we have a movie object, cuz now I'm gonna say, give me a form. And the purpose of this form is to create this new record in the movies table. Okay, with only that change, I just switched it from form with URL to form with model. What's gonna happen to the action attribute?

Let's take a look here. So if I go to add a new movie, look at the source code of this form,[00:52:30] 

it did the same exact thing. Let me prove to you that it did the same exact thing. I'm gonna put an end in here and switch it back to URL and movies path. So now there's two. And let's take a look at the source code of this and prove that actually. So here's the form with url [00:53:00] and here's the new form with model.

And the opening tags are exactly the same with a slightly different authenticity token of course. , but they do the same exact thing. So this is another one of these so-called magical instances where Rails knows or assumes that if you're trying to create a record and this record is [00:53:30] class is, so Rails calls a dot class on this and Rails understands, okay, this is a class instance of class movie.

And if you are going to be, if you're following all the conventions, then that means you probably have a route called movies and that's probably alias as movies. So there must be a movie's URL helper Method, and Rails itself is gonna call that helper method in order to generate the URL for the action of the form.[00:54:00] 

I know Madness, right? If you don't believe me, I'm gonna comment this out. And this out. So that means there's no movies help Path Route Helper anymore, which means we're gonna get undefined local VRBO method movies, path Online Seven. It's like, oh, actually wait. I did explicitly call Movies Path there.

Hang on a second, [00:54:30] go back here, I'll comment these out. So now it's a form with Online 12. Look at that. Now. On line 12 it says, undefined Method Movies, path Online. 12. We didn't call Movies Path. Who called Movies Path. The Form with Method saw that this is an instance of class movie and it called Movies Path, assuming that you were gonna re name your Routes Restfully.

But, so if you don't have Restful Routes, then you can't [00:55:00] use this form with Model Trick. So this is why Restful Routes and generally conventions and rails. , the dividends just compound and compound and compound and compound and compound on each other. Alright, so let's go back and I want my restful routes again.

So put that back, put that back. Now that this method exists, now I can use this method. I've got this going and I can get rid of this. [00:55:30] Awesome. I can get rid of this. Now that we get that idea. Alright, cool. So I've exactly replicated the previous behavior with this form with, but the benefit of using form with model is there's now a block variable.

Provided this method now produces a block variable known as a form builder object. And you can call it anything you want to, the convention is to call it [00:56:00] form, but again, it's, it's just a block variable. So you can call it whatever. Now the Form Object has methods called label. Basically it's the same thing, but take off the tag and it has labels called that form label, form text field.

And I'm gonna switch this back to just movie. And I'm gonna take [00:56:30] out this, or sorry, title rather. So we'll put it back to how it was before I took out that, uh, at movie title, the second argument. And let's just take a look at what happens to the source code here. For this first section, we're gonna refresh and it created a label.

It correctly created the content for the label by capitalizing what we put in as the argument. It created a four attribute of [00:57:00] movie underscore title, which is interesting, and it matched that up with the input correctly, which is great input type text and look at the name of this, it correctly did exactly what we wanted, which was create that nested structure cuz it knows that we're trying to create a form for a model.

Excellent. Well what about this though, like previously we had at movie title, this was the, this was to be [00:57:30] used as the value attribute in case of form validation failures and we lost that, right? Let's, let's check out what happens here. If I say description. So, okay, so if I leave everything blank validations fail, put in this.

Wait a second. It works. It still works. Just like before, if I put this in, do that, look at the source code. We still have, [00:58:00] uh, this is the wrong source code.

Hmm, I see It's giving me the source code of the index page because this is after a validation failure. So it's rendering the new template, but it's on the route. Looks like slash movies cuz we did a post to slash movie. [00:58:30] So it's doing a get of the source code of slash movies. But I need this. But in any case, you can see here, if I inspect element, that'll be a better way of doing it.

It did a value attribute and it populated it with what it, what it had before, so it's correctly pre-populating. This box rails does it automatically when we use the form with helper for a model, give it a form block [00:59:00] variable. These methods automatically do the right thing of using whatever attributes this object already has.

So if I previously, let's just oppose this object, if I do at movie dot title equals preexisting value, so I'm assigning a value to it and then I rendered this form when the title method here [00:59:30] is called with Tex Field. It's gonna be smart enough to prepopulate. Whatever value's already on that object. So it makes edit forms super easy.

It makes this re rendering super easy after validation. Failure methods, me messages. Okay. Whew. So now this form becomes really elegant. Form dot description. Oops. And this just [01:00:00] becomes description. We can get rid of this, it takes care of automatically. We can put in any other customizations that we want and we can even do form dot button, and we can even get rid of this copy.

And because this is a smart, smart method and it knows that this is a new instance that we created over here, it's a, it still hasn't been persisted to the database. It doesn't have an id. It knows that, oh, oh, I [01:00:30] shouldn't use the dot tag. I need to get rid of dot underscore tag on these two.

It knows to put Create movie on here because that's a brand new record. If I had already saved that object, let's just for kicks, do movie, do new save. Although that won't work because it needs some attributes. So I'm gonna say title dot, hi prescription [01:01:00] as you can mass signing these and saving it.

Oops. And then I'm gonna go to add a new movie,

undefined. Oops. Okay, so let me, I did that too much in one line. Do this@movie.save and then let's see what it says. Okay, so it's gonna prefill [01:01:30] and notice. That because this object already exists. The button copy changed to update. This is a smart helper. It's such a smart helper because I'm calling it on this object.

This object is coming from here. This is an argument. It knows that this has already been persisted to the database. So it writes this copy for us. Of course we can change it and say howdy and put whatever copy we want to [01:02:00] if necessary, we can override it. As always, default behavior that is override is rails.

His philosophy in life, we're gonna save you a bunch of time with defaults, but then you can then override it. That's the whole resin detra for rails. All right, so I'm gonna go back here, get this out, get this out, and we now have an amazingly concise new and create [01:02:30] action. And my challenge to you. Is use this technique to update the edit form and update action and get it as concise as you possibly can and ask lots of questions as you're doing so, and then generate a new model.

So head over to a terminal, generate a [01:03:00] new model, not a, not a draft resource, only a model rails, generate model. Pick anything you want. Director name string is the default date of birth. Okay? Whatever you want to pick. Pick a model. Some columns starting from just the model and the database table. Build up the entire resource, all the routes controller, and then.[01:03:30] 

The seven golden actions that we did here, but do it in this modern way and get practice at doing it in this modern way for all seven of these actions. One last thing I want to tell you to get you on your way for doing that is for these seven routes, there's a shortcut. Because these seven routes are the standard restful routes, this name naming, convention id, the these names, [01:04:00] this is completely standard for every restful resource.

Therefore, if I, let me pull up my rail slash info again.

So if I go here, let's search for movies again. So we got all my movie stuff, right? If I comment these out now I've got no routes,

right? So now I've got no movies, routes.[01:04:30] 

Resource movies. That's it. One line gives you all seven of these routes. Go back here, refresh, search for movies. You've got it all back. So when you're starting on your next resource, if it's director, whatever, whatever table, whatever [01:05:00] model you generate, do resources, directors,

go check it out. You've got all seven ready to go. Then add your director's controller and then implement your seven routes and, and then your four view templates, and try to use everything you learned for every link. Write it using a link to helper method for every [01:05:30] URL in the controller and in the view time every, for every url, write it using a route helper every A element.

Write it using a link to helper every form. Use the form with helper and practice that at least once. All right. See you on Piazza.

