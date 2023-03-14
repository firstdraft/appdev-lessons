# AD2 Helper Methods Pt 3

**BENP: Document based on descript transcription of AD2 WS 2023 Day 3 Recording.**

## Starting HM3

**Raghu:** [00:00:00] All right everyone, we're gonna get started. Welcome today, two of F two. There's an called medics,

so please, uh, start the workspace process on that assign. We're gonna be using it to just experimenting the starting point of this, uh, project. When you set on will be a solution to [00:00:30] helper methods one and two. So first thing is may glance through that code base and see if you can think of any questions and then we're gonna press

mm-hmm. Any question if you could, um, I explain the difference post, understand the concept, but it's a bit more refresh,[00:01:00] 

so have form,

whatever,

and then I.[00:01:30] 

And so there's basically an implicit entry value. Your method equals get, and if you leave it out, that's the default, but we can also switch it to posts. Those are two options, right?

And then I have an input in here.[00:02:00] [00:02:30] 

I call the ticket stop now,

Okay, so if we have a input and then I submit this form, what's gonna happen? Well, whatever the user types, it's gonna be sent to some url, and then the cruise string, and then the value that they type.[00:03:00] 

Okay, what if I don't want this? What if it's a file upload? You can't put it into the url, right? Only short values can go into the url. Not even like a long value, like a blog post. So the solution is we switch post, I'm sorry. If it was get, then it would drove like this. If it's post now the request gets placed to just that action.

A query string is not assembled.[00:03:30] 

However, then you can have file those sensitive things like pathway

small, let's say the [00:04:00] route which said post and banks say like, I dunno, I issued Gap later on in one of the other, uh, templates. Um, people say the routing error, right?

Two route. So they don't, there's no confusion between them. Whatever the request is, will only match exactly the verb and the path Combin. Okay. Um, so I wanted ask before we get started, hopefully you got your helper [00:04:30] methods, workspace, uh, sitting. If you just walked in, find this assignment, get your gift pod creation happening.

I wanted to ask if anybody found anything interesting in Ruby Weekly this week. Hey, um,

hanging out with the, uh, like crackling, which

I think so, yeah.[00:05:00] 

Um, okay. So anybody find anything interesting? I found something really interesting. I wanna show you all, uh, this, I didn't have time to look at this week. So I looked at the, the last week one, which I first showed you, and I found that like one of the core Ruby develop first release, uh, extension, which is so cool.

Imagine. So this [00:05:30] is vs. Code installed locally on my own laptop, not the GI Podd BS code. But imagine if I start to write some Ruby and, and then

100 and then print X times Y. And I was, I always tell you, all right. So many times, almost every other line, when you're building up a Ruby program, it's useful to print the output to make sure that [00:06:00] whatever happened, actually what you thought. Well, here's what the extension does. So I have this command, save, execute, and show the execution.

And, and oops, it like adds like a comment at the end of each line showing the result of that[00:06:30] 

one keyboard, every single line, and then follow what happens, right? If

I dunno something, but

like it'll tell you like, which branch [00:07:00] did it going? Visibil here. So I'm gonna be using this constantly. Probably it's not that helpful for us when we're writing Rails applications because we have the prams and our outputs in the server log and, uh, the browser. But for pure Ruby programs, this is gonna be great.

Maybe it'll be helpful for reals apps too. I haven't tried it yet. Okay, so anyways. That's like a really, that's an example of a Ruby Weekly article that actually is applicable no matter [00:07:30] what your level of advancement is, right? This is applicable to beginners even. And there's a lot of Ruby Weekly stuff that is applicable to beginners.

So keep an eye on it, see if you find anything interesting, and then share

Also, did anybody do any exercises this week? Nice. Good for you. Take your vitamins. People do one per week. We're actually moving pretty fast, so I think within two weeks. We'll, so [00:08:00] it's really helpful to learn Travis Pigs to redo the same things that you've already accomplished in Ruby and that's like a great way to, to translate it all.

Okay. Let us, I have a quick question on, um, you always recommend just kinda doing the next one It recommends or should we be like jumping around exercise? Interesting question for that. It's been a while since I've done it and it's changed a lot, so I guess I would do the one they recommend. Uh, but I'm not [00:08:30] on that.

Okay. So here's my, keep the notes to the project up. Here's my app. And I don't think this crackling has recurred, right? Has it? The mic crackling? There's a little bit. Okay. Okay. All right. Here's the application, the list of movies. And we're gonna keep going, make this a little bit better and learn about [00:09:00] four shortcuts.

So first of all, I want to start to get in the habit of making our maps look better as we're, so we're gonna pull in bootstrap and awesome and sometimes use it while we're prototyping. So the quick, quickest way of getting bootstrap font awesome. Uh, and all the Java success is you put link, it takes you to by design chapter.

And this just has stuff that you can [00:09:30] copy directly into the head of your document, which is in the application layout file. And it'll pull these files, these, uh, CDNs instead of us having to download them and upload them and host them ourselves. So eventually we will download them and upload them and host them ourselves.

But just for getting started, this is the easiest way and I'm gonna paste that into the head of my document, which I'm gonna find in the application lab file. And then I'm gonna auto [00:10:00] cause I stuff and the invitation got messed up. Um, and then

one more step, but looks like that's good. So now you see the fonts change, you know that you connected the assets, correct. Any questions on that? I know it's been a long time for some of you Bootstrap font. Awesome. External sheets, link elements, script elements, CDNs, anybody, any questions?[00:10:30] 

All right, let's start putting it to use. Um, I want to add, so as usual, what I'm gonna do is go to the bootstrap docs. I include, and you know, you can read this, the refresher memory. Usually what I do is go straight to the kitchen sink example here with examples of dropdowns, search boxes, disabled link, [00:11:00] and right here I'm gonna copy the example by clicking this handy button in the top right corner and then paste it into my app.

And this is a good example of something that would go in the application layout file, because we want the navar to appear on every page and be the same on every page. So I'm gonna paste it in, usually just inside the body tag, above the notice and the alert. And I'm gonna auto format again, fix the [00:11:30] indentation, take a look and make sure it showed up.

So there it is, dropdowns working. So I've got my, uh, example nav bar, and then as usual, it's time to start to like mess around with it and make it auto. So I would. Actually, what I should do is make a gig commit. So let me make a gig commit before I get too far

closes.

[00:12:00] Keep my workspace, keep my preview.

First time you load under,

but okay, I'm just gonna make a couple changes before I make my first. So in this whole massive of code, here is the link for this part, the top left. And let's modify that to be something like helper [00:12:30] methods three. Let's make that link, just go to the homepage. So just a slash. And really if we're gonna adhere to our new rule, we want possible not.

So actually what I do is replace this with the equivalent link to put the copy over here in a string and then the URL here with a root [00:13:00] round implemented. And also if we want to have this class on the link, we can conclude options on the end.

Now I have the two equivalent version, right? And help method. Lemme just make sure this works. Looks exactly the same. So really this is, this is how, what we wanna have when we're copying in boots back, [00:13:30] examples. Of course it's gonna be plant, but it's a good idea right then and there to switch it over to the help method.

Otherwise you're gonna have a bunch of 'em all to do all at once. And it's easy to introduce errors then. So I'm gonna do that. And what else? This part of the nav bar is the little hamburger. So you never really modify that. That's what here. So we leave that alone. Here's where the actual nav [00:14:00] links begin.

And then there's lists. And then each of these ally with a class of nav I know and a a with the class of nav link are all of our, our links. We don't want too many now we just have movies. So I just wanna show you adding a nav bar. I'm gonna switch. In fact, I guess, like I said, that's do it the right way.

Use the link to helper. Let's just make it, uh, movies. And it's a good movies path. [00:14:30] And the class on this seems to be no link.

And like pretty much everything else. We don't need anything off now, so got all, all the other items in the lab, but just there, that's it. We'll add more links as we add more resources.[00:15:00] 

We don't any, but I'm just gonna leave it for now. Any questions on the bootstrap nav bar? Bootstrap in general? Copy pasting in elements? Yeah, Jack, just simple question is, is there like a shortcut for like commenting out, not in like Ruby, but when you're dealing with like a layout review file like this Actually my normal command slash we have G's [00:15:30] got a A Vs extension installed for us.

That puts,

yeah, about auto formatting. It's I generally speaking command shift P to bring up the command pallet and then search for whatever you want. And then sometimes if there's a keyboard shortcut, it shows up right here. So something that you're doing a lot start to try and memorize the keyboard shortcut. And yes, auto format is a good one to memorize.[00:16:00] 

It'll be different from mac and windows. So control ship P on windows to bring up the pallet. Command shift P on Mac, those are the most, the two most important ones. From there, you can reach everything else with this fuzzy search. Alright, let's make a get commit.

Thank you.[00:16:30] 

I guess because [00:17:00] part one of the homework for next week is we gotta start learning actual git, not the slash GI interface that we created for you. For rapid one, most developers use command line commands and you're gonna just be much faster and more proficient if we start using command line commands. So let's do it that way.

Um, let actually publish one and two on canvas with the homework. Let me just,[00:17:30] 

Okay, so there, there's, in under the assignments, parts one and two of the before week three section are about kit. Let's open up the part two. Oh, that's the wrong canvas. So there should be one about GIT CLI in the assignments list

right here. [00:18:00] We'll look for this assignment, part two and week three before class. And it just has a link to some readings, some chapters about gi And so I'm not gonna go through all of this right now, but all the button click slash kit interface until now did this on, on your behalf. So whenever you clicked on the, it was the equivalent of doing these two commands and typing in the description here.[00:18:30] 

Also, get it, we, uh, it's already a get repost so we don't need to do a get net, but we added a bunch of shortcuts just to make it easier for you to all alter, do this easily. So rather than having to type GI add dash a get commit dash M and then put your message here, we have a shortcut, alias a.

Description here. So let's, right now I'm gonna go into my terminal [00:19:00] and do, get ACM added. Bootstrap a bar. That's

all right.

Keep open as well with the rest of my notes.[00:19:30] 

I've got it.

Um, there's a nice, so if I look at it right now, and if I add, it's like not bad, there's like a green paragraph up there. But let's switch that to be a little bit nicer by using the bootstrap alert. Click on this link to reach the bootstrap alert documentation. And Bootstrap includes these nice like [00:20:00] colored boxes and the text and alert and we're gonna want to use the alert danger for the, the alert danger for the redirect alert and alert success for the notice.

So I'm gonna copy these, let's paste them into the application layout.

We did last time [00:20:30] exhibit first. I'm gonna make sure that it just shows up before I mess around with it. So there they are. Now of course, I want that to be the content here. So who it is should be here and alert should be here. And I can delete these things down here and take a look. [00:21:00] And we have an issue, which is if there's no notice or alert the slide.

So what should we do?

What's statement? Yeah, let's we, let's conditionally render this. Only if those available. If and if you want to, if you're in an EER B template, you can use the, you can start to use some of these zips [00:21:30] and I will send it out to DRB if and tag contract. And then I'm gonna say, if notice is present, which is checking, make sure that it's not, and it's not an empty string.

And then I'm gonna under this, if have.

And then

fix all my [00:22:00] indentation now looks good. When I,

something has flash, it shows up, page it goes away. Looks good. So that's some bootstrap flash. Bootstrapped flash messages here and

pretty nice. Any [00:22:30] questions on this

time? It was, that was a for making engagement, so I'm gonna do that right now. Some, I'm gonna do GI, ACM and then a string containing my GI commit message. In this case added prettier slash messages. [00:23:00] So we're visual slash

Okay, what else? So let's do check now in my app. Everything is like all the way to the edges, and I would like some padding around the content. This is the perfect use case for our, [00:23:30] and we want basically on every page, we want to wrap everything within a digital class container. And if it's something that I want to happen on every single page, then I should put it in your, so between the nav bar and the flash messages, I'm gonna add a Diviv class container.

Actually, I'm gonna do this also. I'm gonna start using app dev. I'm gonna start to show the shortcuts that I use when I'm really writing code it slow way. So you also, I [00:24:00] want add with a class of container. The quick shortcut for that is do whatever element you want, dot whatever class you want. And then hit tab to accept the Emmett abbreviation and move stand out open tab class.

And then move this down below everything else below the yield even. And then auto format. And I've got the container first thing, which is just below the nav [00:24:30] bar. And then within that, the first thing is the flash messages, and then my view templates will be pasted in there so that now we have breathing from here.

We can see that we decided to constrain that. Notice the flash message. Also within the container, change it. We need the, and the start of our content. [00:25:00] So let's add like either on or a margin on the nav bar. Kinda like margin top on the Diviv class container. Maybe we'll do like a four and see how that looks.

Yeah, that looks nice. Looks like a kind of symmetrical space between this and this, which I kind of like. So we'll go with that. [00:25:30] This an example of utility classes that we start by ourselves to. If we need a value, like a margin that's like much bigger than that, we'll have to start to write our own css.

But for the most part, the five or 10 options that we start will get percent of the way and lead to having a more consistent us, us choosing the values white space that we need and [00:26:00] make add.

And that's now, let me give you a second. If you need to, there's, at the very bottom of this, there's a link to solutions in a poll request. So like everything that I'm gonna do today is you can view it all here, kind of the line by line changes [00:26:30] between the starting point and the final result. Now, you know, kind of build up incrementally so it will make sense.

Results.

See what we ended up with. All right.

Solutions.[00:27:00] 

Yeah. Yeah. If you think it's better for my own self

rather than Cause And that's why we have the recordings too, right? To ask the questions while we're together.

Uh, okay. Yeah. Question mark. [00:27:30] It's just the name of the method here. It's just the name of the method. So like, if I took question, it'll be an undefined method present. Does that make. It's, it's, it's like, it looks a little funny, but just think of it as if I'm trying Hello Capital,

right? That's not the method name. So then it's [00:28:00] undefined method. Similarly rails adds a method to strength that is present with the question mark. It just happens to be the last letter in the method name, but no special functionality and it will just return true or false. So if we do nail false, you can also do dot blank, which is, but [00:28:30] the nice thing about this versus just checking, so imagine I have a variable, right?

I don't know what, what's in it. I could check. Is it equal to nil? Right? So why don't I just do that? Well sometimes get a value that's like an empty string. We still don't want to count it. And if we just, that it'll be like, it's not the, it's not equivalent to N so it would say false. So that's right. The present method is smart and it can check both nil.

And is it a empty [00:29:00] string? And it's even smart enough to check of like, oh, is it just white space in here? Then it still, uh, blank. Yeah. What my question some, some of our languages use for volume be,

uh, no, that's not the ruby. The, it's just literally a naming convention, a method. If you're defining a method that's gonna return true or false, then [00:29:30] the convention is end the method name of the question. Yep. You explain what role equals is doing there. Here this has to do with accessibility for screen readers and other types of like machines.

Reading your app, your page. So this, if somebody's visually impaired user is visiting your site with a screen reader, the role attributes help the screen reader know how [00:30:00] to navigate page. And sometimes, sometimes it just tells the screen reader like, oh, you don't have to even read this. Sometimes it indicates to the screen reader that it's an important thing to read or out loud like this.

So that's, that's about, we haven't talked about it before in app dev one cuz we're just trying to like get, but yes, in a professional actual you have to do a, to make sure is accessible. Uh, rails has a lot of helpers for that, which we can talk to. We'll talk authors of bootstrap [00:30:30] prioritize accessibility very next.

So most their examples are gonna include all of that stuff. We just. A lot of little things. Usually I like, don't worry too much about it when I'm prototyping, but before I ship it to real users or especially real customers, I'll hire a firm to do an accessibility audit. And actually a second question. In the, um, in the conditional logic, there's [00:31:00] no like verb that sells, um, the program to do div class E equal, right?

So it just, I would've accepted a p or A due or something like that. I mean, that's that source separate from, um, the condition logic, just generally, whenever we're embedding anything in a view template, the thing that tells to print print is the presence or absence of [00:31:30] a equal sign right there. So if we're using, if we, we, we, this would be the control flow, but we don't want it to actually affect the HTML source code.

So we're using the non output version here. We, if, if this runs which, and this is true, then it's going to execute this code. And then we wanna put the actual text of the notice into this dib. So we'll use the equal sign. Alright. Yep. Um, is there an advantage during notice stop present instead of saying if, notice [00:32:00] if, if notice in that case then, uh, The empty string will count as true.

The only things that count, just so if, whatever, right? The only things that count as not true are nil and false, but everything else, including the empty string and string counts as true as far as if it's concerned. So that's the whole point of that method.

[00:32:30] Yeah. Um, on the files we're pulling from, on the edited new pages, it had a condition at the top for movie errors that seemed to be overriding. What? The trap css. Is that because it's in, uh, yes. So like we're style. Mine was still showing the style color, red message. Is that because message is separate from alert and, yes.

Okay. This, this is the AP accurate [00:33:00] object that we tried to say. That validation failure were saying gains this errors array, which to turn English string. So what went wrong? We're looping through that. This, uh, blue pier drawing a paragraph. All of this is totally separate from the reader. The, the cookies that get.

From Redirect. Right. Okay. Totally separate. So yeah, what you're suggesting is maybe we should use Srap alert here too. Okay. But there's no way to catch the application file because it's [00:33:30] conditional justice

template. So however, that does lead us to our next topic, which is sometimes we have code that we want to reuse, but not in every single template, but in some of templates. And it would be really nice not to have to duplicate that code and then if we change it, have to change it in all these different view templates.

For example, [00:34:00] right now, given all the work that we did on edit and New,

here's the edit on the left and new on the right, what's different? Literally nothing except for the heading because we switched to using the form with helper and given all the stuff that form with does for us in terms [00:34:30] of like, it knows how to prepopulate an input if the object already has values. So we don't have to do that manually ourselves.

The difference between the edit form and the new form when we wrote ourselves was edit form. We put the value attribute in to prepopulate all the fields. The action was different to point to the update action instead of the create action. But the form width figures that out automatically based on whether the object is already saved or not.

And even the submit button form is gonna do if, if it's a [00:35:00] brand new object that's never been saved. This is gonna create a button that says Create movie. And this will be a button that says Update movie. So literally these 20 lines of code, 40 lines code are the same. Now, what if we add a new column?

Column? Let do that. You do this, but lemme just demonstrate that if I add a new column to my movies table, add, I don't know. [00:35:30] Uh, image.

Okay. Add image URL to movies. And this, I'm gonna run this migration real quick. Now I've add So now, oh, I don't have the, Ooh, that's [00:36:00] not great. We should add. You think we should? We should, should we preconfigure vanilla rails with annotate? Maybe It's a good moment to teach what annotate does. Uh, We don't, the gem that we used in app dev one that automatically put those comments at the top of the model that showed you what all of your columns were and if there's any uniqueness and all that, that's a third party gem that we would put in for you.

Okay. doesn't happen. So if you want to have [00:36:30] that, it's really helpful. I'll point out the gem later. I don't want to spend time right now installing it. But the actual way to see what is in your database is the DB schema dot rb file. This is that. This is the actual , the sum of volume operations have produced in your database.

So I can see here that I have a movies table and I now have this new column called IMA url. That's [00:37:00] a string. Okay. So great. I have the column in my table, but if I want to now use it, so if I go to,

I go to my form, of course, I'm gonna have to add this myself. Yep. Quick question about the schema. Rb. Yep. So if, let's say you wanted to like edit the data type or description, [00:37:30] you did the edit thing,

would it create like another, this edit table, or would it update create. First Pointable manually touch this file. This file is automatically generated when we run rails. Do we migrate? So if you need this to be a different column type, don't just change it here. That's not gonna do anything. What you need to do is create a new migration that will change that how type from what you want from [00:38:00] rolls, migrate, update schema, rb.

Or if you don't really care about your data, you could go and like change this migration, which we ran to add the column, change it here, then rails DB drop to destroy your database. And then when your rails B migrate, it'll run all of your migrations from the top and then it'll uh, change. Change. Now it's anything cause it's already been run, [00:38:30] so I could roll it back.

This will the most recent then board migrate and now it will be the right thing here. Okay. No. What if I want to add it to my form so people can actually use that column. Right. Generating our, adding a column is not gonna change our view templates or our controller. That's up to us. So I would, [00:39:00] if I wanted to use that in a form.

Again, you don't have to do this, I'm just demonstrating. I could add. Image u r O here and it'll show up in the field. If I try to populate it, it doesn't show up here. It did save the movie. I don't have a column in my index to show it, so I should do that too. Let's add another [00:39:30] url.

C. We can see movie that I just added. The fifth one, Ima URL did not get Spanish

when I add a column.

Yeah, it have to do with controller. You to add thatt. [00:40:00] Remember this in actually assigned that value to the column, right? Well, yes I did because I started to use this new technique of mass assignment, right? So because I used the form with helper, all the inputs that were in that form, Gary put sub hash in the prams hash.

Yep. Yes. So it's because of this part here, this is where, this is security, that rail, [00:40:30] it only allows one you explicitly say can be through because stuff, so if you. Seven column. You add the column, you add it to your form, you test it out, it doesn't work, you forget, you like bang your head against it for a while.

Maybe you look in your server log. Finally

at one point they, it's so common that highlight this red to make it easier to spot in the server [00:41:00] log. And you're like, oh yeah, right. I got got, let me go add it here

and then now it'll work. Hopefully let's add a new movie. 1, 2, 3, 3. Fantastic. Yeah. Question five. In the homework we added that director's, um, model and we already had a movies model. Now I have a director's model. Um, what I didn't do is I didn't create like a column [00:41:30] saying IDs of the movies that that director has many of.

Do I need to create that column and migrate that in or do I just add some, has many statements matter fundamentally, so it's hard to know sometimes now where are there, what happens that and what doesn't. But the data model is still up to us, so we have to add the column to the movies table. And then if we have any existing movie records, we need to go through and [00:42:00] write a script.

To put the right value in that column, then as many as purely about giving us convenient ways of working with that data. But it doesn't actually,

I, um, it was pretty similar. I, I wanted to create these association when we already have like the two tables, but we would need to change, uh, in terms of the, like the data model, but also in terms of like the white list, [00:42:30] like, like director ID for something list. Yeah. Added image url. I would add a column, direct Id make sure during the, uh, strong parameters and then I'd add like a dropdown or something for the user to actually fill that out in the form.

Okay. I, I, what we were discussing before of the migrations, we would need to create a new migration file for the new association. You [00:43:00] need the form of key column, right? Add a column, whether it's an image, url, or director. Any column you have to do a migration to add the change. Yep. Because we are using all the shortcuts here real quick.

So I'm going to add

thanks. Okay.[00:43:30] 

Directors, then I usually, it's easier for me to check it out.

Alright, five directors. Oh, the CSS got messed up. That's because the scaffold generator generates the scaffold. Do CSS style sheet for us to make it look a little bit better. But since we're [00:44:00] using Bootstrap, we don't want that. So just delete that. Okay, so directors, I can add somebody. Frank . Great. Got Frank.

Now my movies though don't know anything about directors, right? So I have to add the foreign key column rails, generate migration, add director id.

This is a super shortcut way of [00:44:30] generating migration and auto writing the code in that migration all at once. And then reels, do you migrate This is this, adding a column is in the original AP Dev one actor record chapter. And now if I look at schema dot rb, my movie has a direct id. Cool. Now I need to update my form.[00:45:00] 

Director ID

is this one now It worked and ah, I literally

moving

director id [00:45:30] now. I should be able to add a movie

and I'm not showing it on the index page, so I should show it.

Photo format, that very last one got the direct id. And [00:46:00] because we're using forms, it's pretty easy now to make this experience a lot better. I could do form collection, which takes the arguments of an array of active record objects

and the attribute that should be saved and the. Attribute that should be used as the content of the dropdown request. And now [00:46:30] nice dropdown another,

um,

create, add a new movie. Now I have my nice dropdown. Super nice to do stuff like that. Now with these and the values and the ideas and everything manually all yeah. Director's controller, you, you don't have [00:47:00] to wait list anything. The director's controller's not even touched by any part of that flow of a,

okay, so that's cool. Here's what I was getting at in the first place though. We improved this with two new inputs and director with the fancy drop, but my edit form [00:47:30] doesn't

have to go copy paste the stuff that I just did in here. And because it's form, it's literally the exact same. So I could go to the edit and just replace this and it should.

Too white [00:48:00] listed here. Gotta do this here in the update action as well.

That should be see

seven. Switch it to, right? Okay, so now it's showing up. Uh, I should

improve the show page too, but, okay, here's, so [00:48:30] notice all the things that I had to, like, I had to allow the new attributes in both the grid action and the edit action, right? Update action. And I had to copy paste the, the form stuff. Let's see how we can like dry up that repetition first folder. This here, where I'm defining a variable called movie prams and then assigning it.

This code is replicated in two songs. Its [00:49:00] the exact same code. I'm going to try it up by defining a method. I'm gonna call this method movie prams,

and I'm going write code here and get rid of that . So now imagine what happens when we get to. We tell Ruby Movie pers Ruby's, like is that a local variable that was created within this, this scope? Nope. [00:49:30] But it also checks to see whether it's a method defined within the same class that, so this is the equivalent of self do movie paras to run this method over here.

This method over here now is gonna do all the work of getting that subhash out and then method right in the spot that we want it. And then I can use this, I think both spots that [00:50:00] we're doing this work

and if you leave out the self dot, that's the implicit receiver of any method call. So if this is not a local variable, before Ruby gives up and crashes, it tries to call a method by this name on self, which is the same object that this method is within. Okay. So that means

where if I add another column in the future, I just [00:50:30] whitelist it once in the permit method. Here is this one where you have to have like the movies like ahead of it in the file. So it could be on the very last line would still, that's it's not actual action controller. All the methods we define. To help us write actions, we put them at the bottom and they're given a keyword called private that has no functional[00:51:00] 

methods. The main point of a class are called the public methods intended for users of that class to call. Then all the little methods that we use in order to build those are called private method. Come on here. Great. So, yes, so that's one nice thing we can do. And the other nice thing we can do is we have , we can, this is, and this is kind, the main topic of today's class is a technique known as partial view templates.[00:51:30] 

So we can break up our big view templates into little part partial templates. Uh, ran over. So here's, I'm going to, well lemme just demonstrate to you how it works. Before we do it for real. Uh, here we, here's going to the official documentation getting started. Okay. So if I create a file, I'm [00:52:00] gonna create a file called App View zebra giraff.

But notice the key difference here is that there's an underscore at the start of the name. This is review template as opposed to a main, a regular view template. You don't have to type along with this if you don't want to. Just maybe watch what I'm doing. You can, if you want to experiment with it, but I'm gonna create a folder.

Called,

called draft repeat. And in here I'm gonna say [00:52:30] hello from draft. And then in my view template, let's just say the movie's view template, I'm gonna render. So I'm using the render method just like it did in the controller, but here we says the name of a partial view template, the folder and the file name.

But notice rendering it, I don't include the underscore here. The underscore is implicit because we're calling the render method for a view rather than [00:53:00] a controller. So it has to be a park render here. You can't render like a real, a big view template from within another big view template that will give us a result of Hello from giraffe here.

And you can call this as many times as you want

inside the same template. So the fact that we can pretty much ex extract if we have [00:53:30] like a, if our templates are starting to get massive, which they are, they will very quickly. When we start to go down the bootstrap road, you start to have thousands of lines. Of code in a template and it gets very painful to navigate around it and just understand what's what.

So this technique allows us to break up our big templates. Immediate example that I always do is my application file starts to get really big with like, okay, I copied in and then there's a huge nav bar [00:54:00] and then there's the flash messages. So let me organize this. I'm gonna create a partial, usually I make a folder called shared and then there some partials, one for my flash messages.

H hml dot RB page. Send stuff from here. Here, auto indent. And then here I'm just gonna [00:54:30] record, share flash messages and let's make sure it still works.

Yes, so it still works, but I just understand now like the major parts of this template. Similarly, I'm almost create, uh,

that bar, cause this ends up being massive. [00:55:00] And put that in here as well. Underscore that.

That bar still works great. And I also usually create one. If I have all this like CDN stuff, no, I don't need that. Just the CDN stuff I usually put into another one. CDN assets dot html dot [00:55:30] rb case that all in auto indent. And then get it back with, I usually put that above the style sheet link tag because I want my own CSS to take priority.

Also, I think I just learned this recently, the meta care set tag is supposed to be the very first thing in the h l document, so [00:56:00] this should go here even above the title and everything else.

I just learned this because apparently it needs to be within the first file so that the browser knows which character set to use before it can do anything else. So today I, uh, this, look at this now my, my layout file is so much nicer now, right? And you do this a [00:56:30] lot. I'm gonna start to break up our big view templates and give really nicely named.

Uh, we use really nicely named partial view templates to make the code easier to understand. Okay. Let me give you a second to try to do that. Yeah. Danny, is there a, uh, explicit best practice around how we tell the path? Because I've had issues where it needed to know one level above in order to know, or, or [00:57:00] it gets kind of messy.

Well, it depends on the specific example, but when it comes to the render method, we never have to specify app slash use because all use are gonna be located in there. So we never have to say that part. But then usually we want folder in the, sometimes there's some like rails defaults, like if you're in the movies [00:57:30] controllers, you're have to include the folder.

But my suggestion in that one, were too suggest always include the folder in the file because eventually you're gonna from, and then that shortcut will not work anymore. So my rule of thumb is just include both, even though sometimes you're able to drop it. Okay. And see, you can clean up your application layout to [00:58:00] match, match mine.

Template.[00:58:30] [00:59:00] [00:59:30] 

Questions about these partials far. We have a lot more to learn about partials. We're using them super heavily for the rest of the quarter because our main goal for first quarter class is getting to age X, those partial partial age updates and being able to render a part of a page in a partial crucial to being able to achieve those partial page [01:00:00] updates as well.

So they have so many benefits. You can make your code more modular, easier to read, but also be what enables us to get to Ax question mentioned.

So yeah, I'll mention it. I don't wanna spend too much time on it, but Right. The way, let's suppose we wrote our own CSS file, right in the past

[01:00:30] public folder. Create the file,

right? Like,

and then once we've done that, it's hosted at My Styles CSS automatically. Anything in the public folder. We'll just. Then we could use that in our editor. Use a link tag. Right. Okay. Another way and probably the more sufficient way, [01:01:00] now we'll get,

and we create our style sheets in here. Anything in here is gonna

all pressing take on all the white space. Put, you can 10 different files to help to keep you organized. Rails will put them all into one file when you're in production mode, which helps. So this is like a pre-processing system known as the asset pipeline [01:01:30] and all of gets included in your document here, wherever this line is.

So all, all the cssc right in that folder will get plugged in if you have, uh, helper with it. Otherwise it won't show up anywhere. Yes.

In this

seven actually stopped using, [01:02:00] use it on anyway. This is a different system known as sprockets anyway. Anyhow.

But if I go back to my. Like these two, these two got render here. The partials that we rendered in the,[01:02:30] 

when I call that render for the partial, it's always giving me back exactly the same partials. Really, really powerful when you can send it data into the market and then that will be automatically used in the output of the partial. If I wanted to have something like this, right? It's got a, a dynamic [01:03:00] bit of information in it, so called

underscore elephant h and I want it to have something like hello, but then not always the same h to be able, if I read through this from my index, the way that I did [01:03:30] works, it's not, it did render that template when it got to here. It's like undefined local but very lower method. What I wanted to send in the value of that, So you can provide an option called locals, and the value of that should be a hash and in this hash all the key [01:04:00] variables inside this template.

And then with the value like this, lemme do one more and show you how it looks.

Person.

We're getting that error.

Oh, okay. Sorry. Uh, I have [01:04:30] been using a shorthand syntax unconsciously that I shouldn't have been using. Instead of saying the name of the temp, the this, instead of this being just a string, it's supposed to be template. Just like we, like, we've been doing this a thousand times in the controller. We always do render template and then the name of the template.

And we have to do that now if we're gonna use any other options besides just the name of the particle that you have to use. The here. [01:05:00] So now

Zebra,

um.

Search in,

which is where this is, isn't it? It was working a second ago.[01:05:30] 

Wonder

here, uh, where you put the person variable?

So I've got two, two elephant and giraffe, correct. Oh, sorry.

This one is that. This one is this. And then in my movies [01:06:00] I'm rendering the template. What's correct? Strange. I'm gonna just check to see if it's that get pod issue sometimes where you, when you are adding files and folders, that happens from time to time. That's the issue. Still getting this issue. It was working a second ago when I was using the short canned version of just this.

So let's try that. [01:06:30] What do I, I'm just having some kind of brain,

right? It happens to you multiple times per assignment.

Yeah, but now Elephant, so the problem is this one, right? Oh,[01:07:00] 

that's, I have render templates. Time change. Then it'll look. So you, that's definitely not the issue with template. Just when I add the, if you have template is the

be very surprising to me. Why? But I trust you. [01:07:30] Wow. Interesting.

Okay. I to this out because even in my solutions, which I just, I never say render.

Oh, that's what it's okay. Sorry y'all. It's partial. So I actually never knew this would work. Interesting. Okay. [01:08:00] Surrender template is what we say in the, in the action to render like a template. So you with using render with the template, you give it the literal. Whole file name. If you're doing a partial, that's when you don't include the underscore because it's implied because it's a partial and now these all will work.

I until this second didn't, I thought that you could not render template from [01:08:30] within a template, but apparently you can. So we just learned something together. Partial that you didn't put partial or template. If you don't say anything, like I can, I can't think of a case when you would ever render a whole template from within another template.

So I think that's assumption is always that if you're calling, okay, that's what that was. So [01:09:00] anyway, the point being here, these are kind of like, so think as like a method that we're calling to get back some HTML that we wanna put into the bigger template. And just like with methods, very often the, it's useful to be able to send some inputs into the method so that the method isn't doing the same thing every time.

It's gonna take the arguments and then change what it does a little bit and send back. So think of this local [01:09:30] hash as the analogous thing to methods to an argument. Okay, now, With this, we can do some really cool stuff. Um, can you populate the locals dynamically? Like I'm thinking if you have a form and you wanna edit the movie, but you don't wanna allow them to change the movie title, edit the info about it, could you do like, get the [01:10:00] person or the movie to be like this movie or something?

So I think generally the answer to your question would be yes. Because if I was gonna try so, because in an edit and okay, I don't, yes. So this is what we started down, this edit exact flow, right? So let's fix that up. Now I'm gonna extract this, put it into,[01:10:30] 

and same from new, actually, I can put this in there too. That would be nice.

Put [01:11:00] the error.

Now my new movie form and

are using the same podcast. If you wanted mostly the same, but then behavior you would pass in, conditionally check and be like, [01:11:30] okay, let's disable this field or not. So I might something like locals disabled and then like pass list of things that I would want to be disabled and then I could use that array to like check and add that attribute.

So yeah, if house being rendered.

Okay, now here's, [01:12:00] here's, this is currently working. We have I, I extracted this form partial and I'm using it in both, in the new this part using an instance variable called atmo. Right? So one thing that we can see right away is that an instance variable that I defined in my action in the controller is to the partial view templates as well.

And we didn't have to explicitly do anything to enable that. [01:12:30] So instance variables that are defined in the action are available in the view. And any partials rented by that. That's oftentimes convenient, but often times not a convenient. So there's many cases where these two actions new and edit, they like they're want to use somewhere, but they might method name, sorry, variable [01:13:00] name.

So let's just imagine we were doing, we're naming our variables in the app dev. One way this would've been the movie and this one would've been like new movie. And they're that the same. Now we're rendering the template. That's assuming like, okay, now it's calling Dr. Movie, which is nil. So now in the new form, if I go change it to at and at new, then it's gonna work again.[01:13:30] 

It's not gonna work because now here the, so I guess never call that very well anything other than atmo. No matter how many hundreds of actions are using that partial. And sometimes it is hundreds of actions that are gonna use a particular partial. Like think of something that's gonna be all over the place, like the avatar for a user or gonna use [01:14:00] it every single action, the whole app sometimes.

So you don't want to be constrained to have to use the exact same instance. Variable names all over the place. But that's cool because we have the locals because say with line variable, I'm gonna pass in locals and say, I'm gonna pick variable name here, fu and pass in at the movie in this case. So now that means that the record [01:14:30] said, define the local variable, call FU and send it in and put this value into that local variable.

So now here, instead of using any instance variable, the partial will itself pick variable names for everything that it needs from the outside world. We define the variable names here, just as local variables, and then be sure to pass them in from everywhere that you're rendering that form. So here they fu and then in this case, the value is [01:15:00] at new movie, but by the time the partial it's gonna from, from all contexts, it gets named the same thing.

So now this works and this works,

uh, in the new action. Oh, because I forgot my locals, the reason. Okay, so I keep getting, I keep typing this out wrong and it's because I didn't even include it in this lesson because I wanted [01:15:30] you to see the long. But if you use a short computer without the partials, then you also don't need the locals. So now swing do the same thing, syntax, which is what I keep doing and running into this error.

You got one I actually avoid doing. So we'll see here that this works. Now we get both of those two renderings doing the exact same thing. I used to use this when I was building Rails apps, but I just type it the long [01:16:00] way because like 99% of the time this being too constraining. So I usually type it all on now, but both of those are available in case you want.

Okay, so partials are awesome. And then even more the ability to pass in locals makes partials incredible. And uh, let's see where I am here. We [01:16:30] did static partials that are always the same and then we're partials with inputs and we applied that to our form and that's great. Column to model table, make rails, generate migration, add, I don't know, released on to movies.

Released on is a date rail CB migrate.[01:17:00] 

And make sure to add it to strong parameters. The hi remembered for once release on and we'll go to the form and release on. We can make this a date. I forget the, remember the helper at theater date Select, is it? [01:17:30] Yeah. Okay, so now I have a nice select here. Pretty cool. And even better, my edit form automatically has it because it's the same form.

The code is the same. Now, that's not all. Sometimes you wanna feel in the new form and you don't want them in the, that you should use the same partnerships they probably want, but in many cases the field are exact same [01:18:00] as the building form. So you can just use this partial reuse technique. What do you think?

Ready? Well, let's say it is a time and I want, yeah, this is good. I'm gonna take a snapshot of my workspace and share it. [01:18:30] So that you can poke around at what I've done so far. Take a break

for the, the main parts, not like the zebra giraffe stuff, but the actual form stuff. And then we'll answer some questions and then we'll press forward from there.

All right, everyone, we're gonna keep on [01:19:00] plowing forward, so if you could find your date

and before we dive into the next section, which is active record partials, anybody think of any questions, anything you want me to clarify or expand upon about anything we've done so far?

Yeah, uh, I have a question about the homework. It was similar to one of the issues that we saw earlier where, uh, one of the, um, [01:19:30] rule actions, I was rendering a template and it wouldn't work if I didn't include templates. I said render. It was the new movie form. I said render error vendor template.

Do you know why that might be? Well, yeah, these shortcut.

Sometimes if you use the secret [01:20:00] for one, you can leave form. But I think if you use the, you, the

I see, okay. That's exactly much problem. Yeah. So is, like I said, this is actually seat in the real communities. I, and also when you're doing partials, the rails community [01:20:30] will oftentimes do this form here where they do that and then they leave this off and then they do this. So that's the most, most common style.

My style over time has been just type , just like type it out. Like there's many cases where obviously I embrace the shortcuts of rails that let you be more concise, but I just find that pretty quickly we have to switch this anyway in most cases. Yep.[01:21:00] 

Do we have form label?

You want to have a partial template for something like, uh, shared slash forms field. And then you want pass in? Yeah, like the, uh, what should we [01:21:30] call it? Field? Mm-hmm. . Or let's just do a symbol. Let me do the, I'm supposed to be using the new syntax here now, so that's an interesting idea. And then literally you want to just have this and then this and

really making me think that's, yeah. I didn't know if you could that [01:22:00] Yes. Works. So we could create a template. We would create it called form field, and then in here we would copy out all of this, put it down here and render it here. Oh. But here is where we would put the field name [01:22:30] local variable, so that we can pass that in

like that. Let's see if it works. Undefined design variable. Oh, interesting. Okay. So because this block variable too from the form, right? That it's using this. So we'll have to add that.

Object, actually, this is too, let's just make life [01:23:00] simple call. Same thing, just passing it straight through with the same name. Then we get these,

uh, then yeah, we could add another, we could put another variable to be like field type and then use that. So I like where your head is at. Like we can start anytime you see something sort of repetitive with only slight changes, you can create a partial and then have to figure out a way to pass. But sometimes, depending on how much customizing you're doing, you're putting a [01:23:30] bunch of conditionals inside the form.

It gets very unwieldy so you start to lose the benefits of it. But like the, for like, the fact that fields are so repetitive, there's a gem like that basically independently discovered. Probably the most, um, one of the most popular gems in the rails ecosystem is called simple form, which does pretty much what you're talking about.

And it lets you [01:24:00] do like just dot input with the name and you don't even have to do the label part. And it expands out the label and the input and everything. It d it examines the, the type of, the column in the database to automatically infer what type of field. So if it's a text column, it uses text area.

If it's a string, it uses type info text. If it's fully in, it automatically does check boxes. So yes, there's a gem that [01:24:30] does that. Cool. And it's like super, it does so much stuff. Like if you need to have like a form for like a parent object and like tags, it's like a liner. All the boxes stuff. Okay. Um, let's think about this.

So I wanna make the show page of [01:25:00] a movie look a little bit better first. So we over to the details page of a movie. Right now it looks pretty terrible and it's, I want this to be in like the header of the card. Not, uh, in this case, I think, I don't really wanna spend time building up the bootstrap stuff, like a tab.

The code in here, I'm just gonna copy it in and then we'll see what it looks like and then we'll talk about it. [01:25:30] So let's go to show a sign. Oh, here. Cool. This is the output. So it's a bootstrap card. I've got the card header, card footer, and a card body in the card body. I have a description list with the attributes and then I have these buttons, right, and delete, and I'm using font awesome icons for those fonts.

So you should be able to stop, paste the example out of the README and have it look [01:26:00] like this. Now let's read code and make sureand going here. So we got, that's the outer container that has a board around it. Then you have the, the body and the footer. When I'm, I use bootstrap card a lot and I think of it almost like as contain,

you have a head, a bonder as like children of [01:26:30] card. Just gives that kind of great background. So usually you just have some text in there, similarly with the footer, but then the body, you're gonna have a whole bunch of markup inside, including starting on line 23. All of this is what I needed to achieve, these two side by side buttons that take up the full width of their bootstrap row.

Okay, so it's bootstrap there. [01:27:00] Any

boots?

Um, the card is centered in, uh, in the middle of the screen. Mm-hmm. and, uh, is, was that done by creating empty columns on either side or is there a class that just has it centered in the middle? So actually centered it width, [01:27:30] that's a container. That's right. It's just taking up the whole diviv dot container right now.

So you're, I don't actually like that. I want to center it. Let's do that now. So here's my card. I want that to be like, let's, in half or two-thirds or one-third of the page, I'm gonna do a bootstrap row, right? Cuz we already have the diviv dot container from the so not strap row. I want to have like a, let's say call dash MD dash four.

So one third of the [01:28:00] page. I'll put that here.

And now, now this whole card is inside this cell. Now it's like, okay, it's on one third of the page, but I want it centered. So I need to either put an empty cell over here just to push it over.

You can achieve the same effect with the offset MD four class. That's like the same as [01:28:30] having an empty cell to the left.

Six by three,

and then on the phone it just pops to being full width again. So why would you create a diviv that contains the card instead of just adding another class, which would be call empty six within the card question? [01:29:00] Uh, if I have another one here, right? So let's say I'm actually using all 12 of mine or two.

Uh,

okay, so now I've got six and six, right? See this six in the middle? Where is that space coming from? Well, it's because the, each, the, the cells, think of it [01:29:30] like the table cells, right? Solid gutter between each of the cells, which usually we want or, and, and, and, sorry. It's, I think it achieves that using padding.

If I just put the class like this, just try it reasonable. I think it's right. So the [01:30:00] philosophy is, Should be sub separate from the content. So just build out your whole grid and only have grid classes on the data that are meant to be used for the structure of the page. And then within your cells, you and then bootstrap will take care of responsiveness and spacing and gutters and everything else.

Right? So usually when I'm building a page out, I [01:30:30] write the grid,

actually equip tag, then I put content into each cell

and I wanted this to be

one.[01:31:00] 

Alright, cool.

Gives you the option, you gallery mode,

template layout that we have there and then red when they clicked it, trailers the next plate. Yeah. Think there a bunch of ways to do that. Like you could, for example, perhaps out here for like [01:31:30] you. Like gallery or whatever, and then, and see what, and then I might select it,

maybe have a cookie, and then just for every page to visit after that. All right, great. Now that we have, or now that we have the show, [01:32:00] what if I want on my movies index page, what if I want cards for all the movies instead of this? Yep. Should we put all that HDL for the card, the actual show file? Yes. We have partial.

That's a great idea. Because what, like the problem in front of me right now is in another place. [01:32:30] I want those cards, right? Copy, paste it, go here, copy paste this card, go to my index and,

and I'm gonna,

so let's

can keep the loop, but then inside the loop for each movie. I [01:33:00] want a card and this I just copy pasted. So this instance variable at movie needs to change to

here, but now it works. No, I think cards doesn't look great cuz it's like too wide. But we'll get there. So I can [01:33:30] start a dim and then,

and then put each of these cards again in a call and be, let's say three this time.

Now I've got like sort of nice cards wrapping pretty good. [01:34:00] But we have this problem now that we start, as you can see now that we start going down the bootstrap road. This 37, this sort of like the representation of one movie. And those are gonna grow to be like hundreds of lines long once you get really deep with styling.

The HTML repre representation of a record from . So let's not exactly the same and we wanna render it on different.[01:34:30] 

Create a new partial call card, put all in. And again, we don'ts. So that's good. This is just like a self-contained partial now with partial a local movie. And that's what it's gonna use to populate this thing. If I [01:35:00] to my index and here render Marshall movies movie card, and if I just leave it there, it's gonna crash because in the, in the partial once the variable called movie, which we haven't sent, so we'll do local, and this is where it starts to get a little confusing.

But we have movie, movie, movie, movie, [01:35:30] movie, movie,

Movie, movie, movie, movie, movie. Imagine if I called this partial movie too, which is usually what they call it. But I'm trying to keep things a little bit separate. But here, this is the, the value that we're passing in. So I could just do like movie dot last here and it's gonna draw that point. Data, this, the value that.

This is the [01:36:00] variable that the part seconding us to send in. So here, and it usually ends up being that this is the same as this because there's a singular version of this. But now I can go to my, I'll render this partial, and here in the sun it's atmo is the how we get the value. Now this should work.

Click on, [01:36:30] go to the show page. Both the show page and the index page are working and they have the same

page. The styling of it. Nope, I guess that's not the class. But

point being like that partial is being used here and here, I can just continue to refine the styling of what a card, what a movie looks like, and the whole, my whole app [01:37:00] doesn't have to know about the code for it. So this is,

I would say like I use partials a lot heavily for so many reasons. Like I said, first of all, it helps me break up my huge templates into smaller and more manageable chunks. Another thing that's really nice, imagine if I want to add a link to the nav bar. I need to go to the application. I need to [01:37:30] find it in application layout, right?

Here's what I want you all to. So you go over here and you like dig through your stuff and then click on this. Scroll more and more become professional developers, less and less on our mouse. Wanna try to learn more and more keyboard from us, because that really does dramatically change your productivity.

So instead of clicking on a file in the sidebar from now on, [01:38:00] do command shift P, sorry, no, that's for the pallet. Just command P. So just command P brings up the file search and, and then you guys start to just type a few letters. Let's say I want that movie card. I'll be like Mv C D. And it almost always finds it.

And you don't even have to, it's not, you don't have to like a literal match either. Just type a few significant characters and it's really good at ly finding it and then hit return [01:38:30] and it jumps you right in there. So you notice, like I rarely dig around the sidebar routes. Oh, or ut boom movie boom. It's incredibly easier to get around Now that you, I mean, of course it relies upon you knowing what file you want to go to, but now that you start to know which one that is another.

To break up your gigantic view templates into partners. Cause [01:39:00] now I need to add lead to the nav bar. I can just go nav bar cause I create a partial called Nav bar and I'm, I just have what I care about here. So it makes it a lot easier to get it on your code base as well if you create smaller, more modern files, gigantic view templates.

So that's a huge benefit is the ability to just break up your big view templates. Another benefit of part of partials is something like a form here where you can pass [01:39:30] in input, mostly the same but has slight differences. But I would say that's biggest benefit is most of what we do as crud web developers, is we're getting data out of our database and then putting HTML around each record.

The ability to use a partial to represent a particular database record and then reuse that across our app is [01:40:00] the biggest win. I think I, I hesitate to even show this part, but I'm gonna show it to you because you're gonna start to see it when you read Stack Overflow answers and other documentation. So here is the cool thing, don't, I don't, maybe don't even try to replicate this.

Just when you have an active record object m. All active record objects inherit a method from application record, active record base called two [01:40:30] Partial Path, right? So all active record objects have a method included already outta the box and it returns by default the table slash the singular version of the object.

So plural, singular, we go right? Watch it. So I could go into my movie model if I wanted to and add a method def to partial [01:41:00] and say movie slash movie card. Basically, you're able to announce the active record object using this method. What is the name of the functioning that I should use to render you?

And the active record object will respond. That means that, that when I'm rendering it, like in the show page, [01:41:30] there's a shortcut as you might expect. I can

describe the object.

The render method. You give the render method an active record object. It's like, oh, okay, you want me to draw some H M L, the H M L representation of this active record object. So what the render method does is it implicitly calls two partial path on this, [01:42:00] and let's see if this works. Is this gonna work?

No, because the partial wants the local variable movie, which we have here. So the, I dunno if that's gonna work. There's that correct. Okay. Now let's suppose I did the conventional thing. So I, I kind of on [01:42:30] purpose named this movie underscore card. The conventional name for an active record object is singular underscore singular object name.

So at underscore at movie. So now that means that I don't have to overwrite this because the default method returns movie slash movie and I'm ready here. I don't have to pass this object in [01:43:00] either, because it will automatically assume. That the ver, the local variable name that we're using in that partial matches up with the class name, which is the case 99.999% of the time.

So now literally in order to render that partial, you just say render, give it the object. Kind of like how there's the ultimate short form of link to movie and it like figures out using the class name and the named routes and then [01:43:30] brows file. As long as everything matches up just right, you can send link to Mo and it figures out to create the whole A element.

But then this is like a lot more elaborate than that. But I do use this in my actual Real Rails apps. I style all the time. I want you to see it. You willing capture this on the internet. You can start using it if you want, or kind of write out the partial name and the logo passing in until you feel very comfortable with what's going on.

[01:44:00] Another cool is also this kind of situation. Uh, you can just say render at movies

because this is an active record relation. If you give it a relation, it'll do the dot each, and for each object it'll render the object. And if there's a partial that matches the name of the [01:44:30] object, it all figures it out and it works. So if you just have a collection of things like comments, And the comment is a self-contained partial, you can render the collection and it'll work.

Now, I lost my grid classes, so in this case I probably won't because I want these grid, like I need this in here to make it work, right? This, I'm not just rendering the partial over and over. There's other markup that I'm rendering. So you don't always, [01:45:00] but if you read, um, in the, uh, in the notes for the project, in the official docs, if you're curious, you can read through and there's like so many super short ways of doing this and render a collection.

And you can actually specify a separate template to use as a spacer between each one and put that so they each object and then a spacer and then a the object. So lots of super [01:45:30] ways can be concise. This documentation describes them all if you're interested,

but we'll leave it there for now. Uh, okay, what's next?

Okay, so we did cards in the index. Jump to file. Start using, jump to file more. Copy. [01:46:00] Okay, now I wanna switch gears and talk about something else that we about very briefly in Optiv one, when we talking about siren I out, but I wanna remind you about it. There's another feature in Rails called filters or, uh, uh, before action here, how this works.

If I have a controller and I want to just random method here,[01:46:30] 

and

so I'm printing, if I call this method

and action Action and I look at my server log,

so when you print in [01:47:00] the controller, the output is in the server log. But the key here is that I'm able to call this method here and then maybe let's say if I, if I, if I had a method that I wanted to call,

it's nice for me to, if you have some repeated logic, the exact same code happening in multiple actions. Well, you can extract that log into a single method and then call it as the first thing that you're doing each of those [01:47:30] methods. And if you're doing that a lot, then Rails has a syntax say before, give it the name of a method and then you don't have to even call it, it's now gonna automatically run this before every action in this controller.

Let me clear my server log. Is it like movies index and, oh, what's this missing Partials movie [01:48:00] card.

Yeah.

Okay, so let me clear this. Press this server log. So like it that that method ran before Index and

method ran before edit. It's just [01:48:30] gonna run before every single action in this controller now.

And I wanna be a little bit more surgical with it. I can say. Okay. And maybe not everyone. Maybe we'll just do the show and destroy actions so you can specific actions or you can accept specific actions. Really nice. And the place that we saw it before [01:49:00] was when we wanted to have like a signed in user them.

We didn't want them to do anything until they signed in. So if, and back then we were using exception use. This doesn't exist in this app, but I'm just saying as an example, if this is present, then we'll let them in. If not redirect them to the sign in page,

remember [01:49:30] this. Then we would have to basically need this code as the first three lines of every single action on our app of, there could be thousands of the actions in our app and if we want the same code to run, that would be extremely tedious. So instead we would put that into a method. We'd call it something like force user sign in and put it in here and then we would before.

Right? Great. Now [01:50:00] we would call that call, it would be

now every runs literally before every actually app. Okay. Okay. So we did this really quickly when digital generator, but we didn't really touch it after that. I just wanted to remind you that it exists because you are gonna, again, you're gonna see it when you start to read [01:50:30] Rails. Documentation. For example, in this app, we have some repetitive code in No index is pretty fine.

But here is, we have movie, we're we're taking prams of Id looking up and creating that movie, and we're doing that here. Exact same thing we're doing here. We're doing it here and we're doing it here for show, edit, update, and destroy. The first [01:51:00] thing that we need to do is find the movie and then put into a variable, right?

It's not that bad, but if I wanted to be very lazy, I could take this out, define a method, let's call it, uh, find movie or something, set movie

code there, and then use action to execute it. [01:51:30] But I don't want to do it for all my actions, like I don't need it in new and edit. I need it.

Update and destroy

actions. That's that. Now. Because we're not rendering either. Take it out here and also start [01:52:00] action. Cause I, this is again, whenever you're reusing code in different places, you're kind of constraining yourself. Cause you now have to use the same variable name everywhere. So I don't have the ability to rename this sound.

Yes. Switch this back to at moving. But this now runs, uh, before I reaction, let me see if it works. So edit seems to be working. Show seems to be working. [01:52:30] Update seems to be working and destroy seems working. So it's still working and we've dried up our code just a little bit more. I don't know if I like this.

I just wanna show it you cause you're gonna capture it. I don't, I wouldn't do this in my own code because when my team members are debugging the show action, I don't want them to like go here and be like, oh right. It's not very clear. They have to go and look at the view template and see that, oh, actually there is visitor.

Where's that coming from? And then [01:53:00] remember, oh, the one done is, there might be a before action and it might not even be in here, it might be in the application controller. So there's a lot of stuff that you have to backtrack and check. And I like being very explicit, so I might not use it a lot. Context, but plug users not in, or making sure that the sign user has the permission is like supposed to be able to execute that action.

Those are purpose for candidates for actions[01:53:30] 

and read.

With all that said, now I want us to press together open

and you can use any table name. I give director, actor. Let's do a [01:54:00] name and a date of birth, which is a date and a bio to the text. So you're using the rails, generating the built-in scaffold generator that I talked about, last class generating, and then read all the code that are generated. So we'll generate, gonna do a whole bunch of stuff, model migration, and create some tests.

File source, it puts resources in the routes for us. There's the controller, so you can skip reading the test files for now, and [01:54:30] the helpers and the jbo. There's, you can skip all that, but read through. Read through the routes. Read through the controller that was generated. And read through all of the templates that were generated and try to think of anything that doesn't make sense out.

Cause I think we have not touched upon everything that the Scaffold generator uses. And that's kind of the baseline minimum amount of [01:55:00] knowledge that Rails developers are assumed to have on Stack Overflow and blog posts when people are writing things. So it's very crucial to understand everything that's going on.

Scaffold the controllers, so the one controller, the view templates. Make sure you understand everything that's going on[01:55:30] 

my snapshot. So you're gonna have to,

whatever reason, doesn't

fix it.[01:56:00] 

I send them so you can read my code but not really work in them.[01:56:30] 

The whole question you said has questions or question. Um, yeah, let's start taking questions. What do you think? What do you see? So notice in the controller, its the default blank. [01:57:00] Do you, do you normally add that back in control? In the control of the act? Uh, sorry, the show, uh, uh, functions, please. So you add that back in for clarity.

The reason I just showed you, it's

here, here. And then this is the open scaffold. Everybody, basically, every Rails developer kind of [01:57:30] expects. So like, put it in. I'll, I just like, I, I let that be. Yeah, but I don't do cell like that myself. I'm writing.

Yeah. I changed it. Be good. Great. This is the shortcut. So look at, so when I wrote it, the square bracket and then it's an array of symbols. So for, this is a quick way, just a ruby. This is a ruby thing, not a rails thing.[01:58:00] 

Or I guess just do that in IRB too. But it's just like a quick literal syntax for creating an array of symbols. So you have a column, the colons, and there's a way to do that with strings. Two, I think it's w Um, so if you need an array of strings real quick, and if there's no spaces in any of the strings, you can use this shorthand syntex.[01:58:30] 

Okay. Anything

looks like instead of a button, like a class actions thing, you said button. Something else I used Submit, didn't I?[01:59:00] 

Okay. But I guess

Somem to get you started, Mr. Class, write up Style Rule four if you want.

Yep. Matt, the controllers. What is going on with the,[01:59:30] 

um, ? So one of the things I don't, let me, let me show it to you in the context of movies. So we have the movies. Oh, actually we had it here too. That's good. When you want from that action to be able to send out either JSON or H or depending pdf, [02:00:00] if you want that same resource to be able to request, in other words, you're building an api, not just html.

Then we add the Respond two block. And the way you interpret the respond two is almost like an if statement. Kind of it's, imagine if it was like, if request not format equals html. Elif request format equals json and in each, so [02:00:30] only one of these branches is gonna run. And then here we would say, okay, render the index template here.

We'd say render the index dot js o template. This is just pseudo code. But think of the respond to as kind of statement where it's like, okay, if the request was json execute this block. If the request in this case an empty block because we're doing the default thing of render, uh, movies index, so we can just [02:01:00] leave it blank.

But that's what, that's

which we're not gonna really do a lot, but because it's such an important part of most web apps these days, because you're gonna wanna probably have an iPhone app,

you're gonna want it

with the actor. Couldn't sound that I'm,[02:01:30] 

it's so the format json, it doesn't render show. When you render show it's in for a template that corresponds to that name in the actors and also corresponds to the format of the request. If we look at the templates here for actors will notice. There's two show templates. There's a HTML show template, and then there's a JSON show template.

E r B is the processing, uh, system that we use, [02:02:00] like dynamically create html. J builder is a templating language for JS O. If we look at this, it's like an another like that have to learn, but it's a very first language is creating a JSON response using, using

creating J. So

it's automatically selected because of the format [02:02:30] of the request. What else? Anything puzzling in actors controller or I guess generated, but that's the same as just the model. Um, anything else? So there's the json, the J builder templating language, which we haven't got to yet, but you template building JSON responses.

We got partials here.[02:03:00] 

It's a lot that goes into this. Yeah. Um, this might have been covered before in the edit. Uh, uh, you. It says link to show and then it says at actor instead of at Actor Path. I can't remember if that's, so if I expand it out, it would be actor path and then I [02:03:30] see. But you just give it an active record objects kind of like the render thing I just showed you.

These methods, oftentimes given an active record object, can put together the rest as long as everything is named conventionally. So you have to have a name drop, helper that match name class, and then it can do it for you.

Um, yeah, so good here. [02:04:00] So I, I want it to kind of rush to this. When I learned rails, you guys, my teacher showed me the scaffold generator as the first thing and then like never built up to it like us. So when me and my cohort, like it was amazing, right? It's like, oh my gosh, you just run this one command and you already have old working app, basically.

But then as we tried to like build our own stuff, our unique value for our app, we had no idea how [02:04:30] the fact that the fact that there's an action that's being inferred automatically by the class of the object and the method poster versus method get, like we never learned any of that. All we learned was like how this method.

What argument facts and then what the output, what the effect of that was. And we'd just be like kind of trial and erroring and copy copy pasting until we got, which is a legitimate way to learn, obviously, like I was able to [02:05:00] learn. But I think hopefully having some understanding of what all software doing for you will make it easier for you to customize when you inevitably have to customize what's going on.

And ultimately, like most Rails developers, when they're learning, they generate scaffolds and then they just copy paste this up when, and they render. Like if they need a form for a actor on a some other page, they just rendered the partial and don't really worry about how it's working. And you can get really [02:05:30] far that way.

But in inevitably, you're gonna reach a wall with that strategy and you all can just write a archive from scratch. Don't use any of the helper methods. You know how to drop back down to the basics and wire it up and just make it work. So under, remember that you have that in, in your back pocket at all times.

But maybe now start with the helper methods and try to make them work [02:06:00] and try to learn how to force them to do what you want 'em to do over time, it'll become second nature for you.

All right. So like, yeah, just remember like I went through all this fast, but most of the time you're generating the scaffold and the code gets written for you, and then you just have to be able to copy paste it and make it do what you want in different contexts. So if it feels like it'd be hard for you to sit down and type this all out from scratch, that's fine.

[02:06:30] It's hard for anybody to type up and scratch so many types stuff from scratch. We generate it and then you need to be able to know how to modify it and customize it. All right, so that's all I wanted to cover today actually, no, one more thing. Sorry. Uh, the other thing that we're gonna is every app that we build is gonna need users and sign in and sign out, right?

So in the old days we wrote it by hand and then we got the draft, [02:07:00] which just wrote it for us. Now we're gonna start using called device. And this is the gem that pretty much every, like I would say, 80 plus percent of rails apps, this gem to build the signup system,

I'm gonna add check device, and then I'm gonna bundle install,[02:07:30] 

and then I have to run a command to install it. Generator device install and it adds files. This is, this is Aran a locale file in case you wanna translate to,

but now that I've installed that gem, I can use the device generator instead of draft. Cool. An [02:08:00] account, the rest of it's the same as always. It's the model name and then any column names in that table other than emails automatically because it's meant for sign in. Signout does a whole bunch of stuff for,

and in the route manage one line devised for users. That one line expands out into like 15 different routes [02:08:30] or sign in, sign out, edit profile, cancel account. It asks functionality built into it. The reason we're gonna use this gem from now on is like, what if somebody forgets their password? Well, I would, I would send that an app dev one.

Well, hopefully they have your phone number and they responsible, and then you update your password for them manually. What's something they tell you over the phone? What is the actual flow space you like? Oh, well, there's a forgot password link, which you click on it [02:09:00] and then it goes to another form where you type in your email address and then it sends you an.

With a random token that then they click on and then we verify that they have the right token. Then we give another archive type new password from the new password and then it updates the password. That's a lot of work to fill all those archives, password flow. It's a lot of work and there's a lot of ways to get it wrong and then make your app insecure and hackable.

Rather than that, we're gonna use this. [02:09:30] That means I, it's my app here. I closed it. Oh, here it's, I, uh, have to restart my server because I added a new gem. So don't forget, when you add new gems, you gotta control, restart your server to pick up the new code. The bid server command only looks at the gem file once when it starts up and great.

Now I have users slash [02:10:00] sign in and this archive and the view templates and everything in the form for logging in works. And look, there's, I forgot your password. This, and there's a thing and it will your app to a mail provider like mail gun, mail gun, that's not very robust. But once you just connect, you sign up for your API token and connect your app to a mail, this whole mobile, which is amazing.

So [02:10:30] I can sign up.

Another ation pattern character validation built in. All of that is configurable.

This is also, um, a, a password digest or that takes, so the whole thing works. Look at my code here with the draft account generator. It created some controllers. [02:11:00] It created a user authentication controller with the device gem. It doesn't even put the controller in here, the controller, it's there. Of course, we saw that the archives are working.

The controller file remains within the gem and 99.99999% of the time, you don't want necessarily the code for sign in and sign it. So put the code here for us, the controllers in the gem. Now, if you need to do something custom, you can [02:11:30] generate, you can ask it to generate the code for the controller, and then you can modify it if you want to.

But like I, I don't think I've ever done that. I've never had to modify the controller actions for sign in and sign up. They're so boilerplate. What we will do though, is we wanna modify the view templates because like,

like this, oh, I'm sign in. I gotta sign out. Okay. So we can generate view templates if we [02:12:00] want to. We can stay. It views,

spits out these views, views folder that we can then like go modify and like add bootstrap and do whatever we want. So this we, we will want to customize how that look and feel of the view templates a lot. So devise is like, sure, here you go. Knock yourself out. Controllers, we very rarely [02:12:30] modify, so generally we don't.

But there are ways can customize those into, there's a chapter here that has more details about like, okay, how do you install it? How do you generate it that? But the good thing is like we're not putting to do much coding at all of it. The only thing we are putting links in our app to the sign in signup page, sign out, [02:13:00] edit profile dev device provides these helper for, so link sign in, new user registration path.

That's it. Can you use these in your templates where relevant, but you don't have to build those arm caps at all. And then crucially, dev devices defines a helper method called Current underscore user. This helper method is gonna be available in all view templates and all controller actions. [02:13:30] We are not gonna have to touch the session hash directly, ever.

We just used this helper method, which is available everywhere, well not in models, but in controllers and actions. And they'll return n if and it'll return the actual user. That'll be site very similar draft account method, uh, think draft account, define an instance, right?

Okay. After that, [02:14:00] you gotta use conditionals. You gotta use before actions to do the actual work of authorization and conditionally hiding and joint things. That's still on you. But devise gets us really, really far with the authentication step, which is figuring out if they know who they are.

Jim Generator included the force sign in. User action devise includes one called authenticate user, exclamation point. [02:14:30] Same, same thing. So I would go into my application controller

if I want to force somebody to sign in before every action. This is fine inside the device controller. So now it's gonna make me, I, I'm already signed in. Me. Okay, fine. I'll give myself a sign out link real quick.[02:15:00] 

It's Destroy User Session Path is the name of the Route Helper Method and we need to do a method delete on it. And I also go and delete the scaffolds dot CSS because it's interacting with Bootstrap and messing up our css.

So now I'm signed out and notice [02:15:30] it doesn't let me go anywhere until I signed. That's it. So very similar to Force User, uh, that the draft account generator gave us. So, okay. Point B device gives us everything that the draft account generator gave us, but 10 times better and like so much more stuff. Like it has little Remember me checkbox so they don't have to sign in every time that they come back.

That would be a bunch of work for us to implement by hand. So we're gonna use device from now on, we're gonna leave draft [02:16:00] account behind us now draft pieces and it's gonna look a little weird, but we just not November, at the end of the day it's just RCA and HTML and peram. But let's attempt to use that from now on and only go back to draft resource.

We really, really need to do something custom. Sound good? Great. Well this is a milestone. So now [02:16:30] this is the amount of, like, these are the main methods now, but you've seen, uh, partials and the form with helper linked to re uh, in the models about how belongs to, that's kind the baseline knowledge that rails developers assume all other rails developers have.

So now you're really gonna be able to start to read Gem re and blog post Ruby Weekly. And you should be able to understand, okay, well your homework is gonna be to into practice, [02:17:00] build photogram yet again,

but you're gonna build it the way that I would build it. Starting like instead of build up incrementally learning something new along the way, and then refactoring, I build it from summer. All the tools and trade I would use when I'm starting to build like a, a client project in this video that will add more performance and security to the [02:17:30] application as well.

Okay? We're building it for real now. There's no more like, oh, I'm gonna ban you by by showing you a shortcut in a couple weeks. Not anymore. You're gonna do it the real way this time. Alright, see you next week.

