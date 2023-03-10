And then we'll, we'll start doing our next project, which is called AD2 two. Getting started. You can start to set up your GI [00:34:30] pod workspace if you finish with the exorcism set up, and then we'll be living in here for the rest of the day.[00:35:00] 

Let us know if you have any issues so we can come pop out.[00:35:30] [00:36:00] [00:36:30] 

We'll do work on exorcism work. See how far [00:37:00] you can get on exorcism problem setting until like 6 45. Then we'll keep going.[00:37:30] [00:38:00] [00:38:30] [00:39:00] [00:39:30] [00:40:00] [00:40:30] [00:41:00] [00:41:30] [00:42:00] [00:42:30] [00:43:00] [00:43:30] 

One more minute for extracellular puzzles.[00:44:00] [00:44:30] [00:45:00] 

All right, everybody. Let's, uh, let's keep going. I just realized actually that exorcism has the solutions that I submitted nine years ago. When I was learning Ruby. And so here was my first iteration of a puzzle called Anagram. So you can [00:45:30] see, you know, pretty decent, Ruby. I mean, I don't know. But I went through, so then I, and I expected immediately to be let through, but then I had to go through seven iterations before they let me go to the next puzzle.

And my from this, so 21 lines to this nine lines. So this is how you learn programming. There's like so much in Ruby, it's impossible to just [00:46:00] exhaustively learn it top to bottom A to Z. The way you learn Ruby, is you solve actual problems and then you share that code with other people and they give you feedback on how they might have solved it.

And you kind of virally just learn everything that everybody else knows if you go through this code review process. So think of it as taking your vitamins and take, do like one or two of these per week and you're going to get better quickly. And if you don't, obviously if you don't get the human mentoring from exorcism, [00:46:30] well that's what we are here for.

You have teachers, so we can just talk about them in office hours. All right, great. Let's keep going. Set up your, let's start on the next project called 82. Getting started. There's a bunch of notes that read me, so let's keep that open by clicking on this blue button. And I'm going to close up a bunch of other tabs

and we're going to start to go through this.[00:47:00] 

Once your workspace is up, do a bin set up just to make sure that it runs all the setup stuff.

One difference between app dev two and app dev one is, is in app dev one. We had kind of a slimmed down Rails project that didn't include stuff that usually comes out of the box with Rails that we just didn't need in ab dev [00:47:30] one cuz it like slows down the setup process and it was unnecessary dead wait for us.

But in app dev two we're including it in our projects. So setup might take a little longer and we're just going to have to to get used to that. But once you do bin set up, let's do Bin Server and check it out. As usual. You're open my app preview and then I'm going to check out Route Stu RV [00:48:00] and we'll see that this is actually just an empty app.

There's nothing in it right now, but we're going to use this to review some stuff and, and think about where we're headed this quarter. So first thing I wanted to remind you all, so these are notes in the Read Me. I'll remind you that there is a chapter. That's like gigantic reference of all the ruby stuff that we encounted in app dev one.

So you shouldn't at some [00:48:30] point just kind of scan through this and make sure that it mostly makes sense to you. I know that for some of you it's been a long time since it took app dev one, but this is the best way I can think of to just quickly review all the stuff that we covered and then come talk to us in office hours, if any.

It seems like Greek because I will expect you to be fairly familiar with everything in here as we start to build out our after have two projects. Okay? Now what I want to do first is generate a draft [00:49:00] resource and just examined that code and make sure that we all feel pretty good about what's happening with the `draft:resource`.

Cuz it pretty much represents the culmination of what we learned in act one. So I want to copy this command and run it at a terminal tab and when you try that, it's not going to work initially cuz it's going to say, could not find generator `draft:resource`. That's because we wrote the [00:49:30] `draft:resource` generator and it doesn't come with Rails out of the box.

And we wrote it in order to make it easier to learn and after one. But moving forward, actually don't want, like after today, I don't want you to use the `draft:resource` generator anymore. We're going to learn more powerful generators that come with Rails. So this is the last time where I'm going to generate one of these.

Therefore we didn't include it in the base app that you cloned, so we're going to have to actually pull that in. So let's head over [00:50:00] to our gem file, which is located in the root folder, somewhere at the bottom here. And let's pull in the draft under generator's gem. Then we have to say, go get that from GitHub.

And the repo name is first draft, draft underscore gender rate towards. So you have to add this line here to your gem file. And then [00:50:30] in a terminal tab, run the bundle install command, or just bundle for sure. And it'll go to get 'em and it'll go install that gem for us.

And this is how we add gen. You've never done that before.

Command here is bundle [00:51:00] install.

Again. This is the last time I want. Well, yeah, yeah. Ideally this is the last time where we're going to use the `draft:resource` generator cuz we're going to evolve to more powerful ones. So, Try to avoid doing this in the future. I know it's tempting because we're very comfortable with the draft generators, but we want to try and force ourselves to to level up here.

So sure, [00:51:30] once you have that installed, you should be able to run the Rails, generate draft code, resource movie, et cetera, et cetera, from the . And this time it ought to work since we pulled in that gem from GitHub and it generates the standard controller for us, our migration, our movie model, and our index and show and some routes.

Let's go check it out and go to my [00:52:00] route. RV can remind ourselves the routes that are remote for us and then we can go check this out with, if I go into slash movies in my app, it gives us the pending migration air cuz we forgot, I forgot the reels. DB migrated as always. I guess in rail six there's a button I can click right there cause it's actually, yeah I did it.

It's nice. The [00:52:30] error message. I dunno if you saw that, but as of rail six point something, the error message had a button in it that said run pen migrations. I just clicked on it and it did the Rails DB migrate for me. Nice. Uh, and now I've got my movies and I can add something.

Oh, and we see our first error, which we're going to have to now talk about.[00:53:00] 

So I tried to add a movie and I got this invalid authenticity token error. I'm going to pause here, make sure everybody's caught up with me. Raise your hand if not[00:53:30] 

the.[00:54:00] 

Better than I am. This

is the repository, which is.[00:54:30] [00:55:00] 

So I.[00:55:30] 

It's like, oh.[00:56:00] 

[00:56:30] Say,[00:57:00] 

supposed to.

This is great. I'm glad. [00:57:30] Shaking off some rust for those of you who's been a while. Uh, okay. So we have an error showing up here That's right. And we try to make a new movie. Before we resolve that, I just want to like talk through how this page is showing up because again, it's been like a year and a half for some of you since you took app dev, so bear with me if you just took App Dev last quarter.

Okay. So the generator wrote these routes for [00:58:00] us in the routes I first visited slash movies, which is streaming the route on Live eight, which is telling Rails when somebody visits slash movies go to the app controllers folder, find something called movies controller, run the method called index. So Rails goes over here, heads over to the app controllers folder, looks for movies controller, which was just generated for us happily by the resource generator.

And then it looks for a method called [00:58:30] Index, which it finds here runs this code. This is referring to the model in the app models folder, which was also created by the generator for us. This is the class that we use to interact with our database table, which has methods like DOT All to go get all the movies in there.

It's got dot where to get particular movies. So we got the all movies and put it into this instance variable with an act in front. We're rendering a new template in the [00:59:00] app views mobiles folder called Index H rb. So this line here is telling Rails to always go look in app views and then whatever folder and file is specified here, which again the generator created for us.

In here we have some HTML and we have some embedded Ruby. This is empty right now. This is coming back with an empty array, so it's not doing anything. But once we add some movies, that will [00:59:30] create a table row per movie in the form that's not working is this form right here where when we fill out this form, it's going to go to this url.

It's using a method of post, which is the key part here. This is something we learned sort of towards the end of app dev one. There's different http verbs they're called and we started out in app dev one using Get for Everything. [01:00:00] Then we evolved to using post when we were adding or updating records or demeaning records sometimes because if we wanted to do something like a file upload or if we have some sensitive information like passwords, we don't want to use get, because it'll put the password right in the query string and the url.

It'll be visible to people who are spying. Whereas Post puts all of the inputs into a different part of the request so that they're not visible and you can have file uploads [01:00:30] and you can have anything you want and you can have arbitrary length. Uh, and we switched to post for that reason. Okay. With what I just went over before we resolve this error here where I try to create a movie and I get this author history token, can anybody think of any questions about the route controller action view flow or any HTML or any Ruby, anything basically that was involved with displaying this page [01:01:00] here?

So this action here,

rendering a template here, got static html, we got forms. So trying to think of anything that's fuzzy about this. Yep. Um, kind of a syntax question. Uh, and a lot of the, um, especially in the, uh, controller mm-hmm. , [01:01:30] there is a, a lot of like brackets, space, colon, kind of variable name where like read their vendor template, let's order created.

Yep. Why is the syntax that way? What does that colon do and why is there space before? Good question. Okay. So this is a method with prees, meaning the arguments are. This method requires some input, right? Call the arguments. So far so good. The curly braces indicate that this is a hash [01:02:00] literal, so we have very stereotypes, right?

Strings, arrays in integers. Decimals. The curly bracket indicates that what's in here is a hash. So far so good cuz we have arrays like this and then we have hashes, which look like this.

And if I have an array and a variable here and a hash and a variable here later on, if I want to access the element [01:02:30] like that, I would say a at 2 0 1 2. And for a hash on say, fetch second and now return this value, right? So they both lists this kind of list. The values are labeled by us and we fetch using the labels, the labels that we choose when we're labeling these values.

Can be any, any ruby object. So I couldn't choose chosen to [01:03:00] use a string like that and then I'd have to fetch using the string. But in Ruby, so like most languages don't have this other data type, starting with the colon. In Ruby we have it, it's called a symbol, basically a string. It's just that it can't have spaces or special characters in it.

We started off with a colon. We don't have to end it with the colon because there can't be spaces. So it just ends when it runs at the end of the token, and usually in Ruby [01:03:30] we use these as the keys in our hashes. In other languages they're called associated arrays or dictionaries. But for labels, we use symbols in really?

So far so good. Yeah. Okay. Now the white space, we don't need, it's totally stylistic. So some white space and ruby is significant. Most white space and ruby is not significant. The only really place usually that it bites people is if you put a space right between the parenthesis, [01:04:00] you put a space right there that's going to mess it up.

Cuz now this method doesn't know what's its parenthesis and what's its arguments and what's coming later. So parenthesis are used for order of operations as well. So that's the only place where you really gotta avoid space is everywhere else. It's almost immaterial, just up to you. Like, we could do this if we wanted to for like you, the line was too long and we wanted to indent it.

We could do that. [01:04:30] Most white spaces ignore. Good. Yeah. Thanks. Any other questions about anything so far? Love it. Okay, so let me go check out these notes again and. Okay. First of all, I want this to work, uh, here. There's so many things we need to learn when it comes to leveling up our code base from what we're doing after f1, which was [01:05:00] easy to get started with, but then like all the little things that you actually need in a professional code base that you're charging money for, that we would never have even thought of in terms of security and performance.

But happily, Rails and tens of thousands of companies that use Rails have encountered these security holes and performance issues and built solutions for them into Rails. It requires us a little bit of extra work to use these solutions built into Rails and after one, we actually [01:05:30] disabled them all to make it simpler for us as we get something up and running.

But now in after two, we've re-enabled all of those default protections, so we need to take a few extra steps to make things work. Here's what's going on here. When I submitted this form, it did a post to

the slash insert route, and now that we are using Post [01:06:00] for our update and create anything, any, any action that we expect to be modifying our database, we're using Post Rails now is going to expect. That post to come along with essentially a password that guarantees that this form that the person is filling out was created by us and not by a [01:06:30] malicious third party.

The reason for that is if we just blindly accepted that request, somebody could put this form on their own website, like a malicious person if they tricked one of your users into filling this form out. But then they put our domain here. So suppose a malicious attacker [01:07:00] put this form on their website, but had it point to around in our website, then they would be able to modify our database.

And that was, that's called cross-site request forgery. It was a really common attack that happened a lot in like the early two thousands until frameworks like Rails started just building in protections against it. The the solution is, in this form, we're going to put a hidden input that [01:07:30] has a password essentially, and we're going to randomly generate a password every time we draw this form.

And we do it in such a way that only we are able to generate those passwords correctly and when we receive the parameters. We're going to check and make sure that it contains one of our passwords that nobody else can. Spoof sounds very complicated. Happily Rails takes care of it for us. We're going to go into this form and add an input in here.[01:08:00] 

Let's start with type equals text. And for the value of this, we're going to use a helper method. So Beson will be right there.

And the helper method is called Born Authenticity Tool. Lemme just make sure that works and then we'll go back to the code. [01:08:30] Okay, so now I have this input here with this like long random string generated automatically for me. This method returns that does a bunch of fancy pants photography. There's like a cookie that it's set, there's a secret key on the back end, and there's a cookie on the front end that it uses all that to create this string that only we know how to create.

And we need this to come into the prash under a name that I'm probably going to forget and [01:09:00] I check this, I think it is, refresh this. So get. See if it works. Okay, cool. So we need to name, we need to name that input authenticity underscore token that that'll make it come, appear in a prams, hash and Rails automatically makes sure that this parameter exists with the correct value for any post request.

Boom. All of a sudden we [01:09:30] have C S R F protection. One of the many things that's like we would never have thought of to build this until we got hacked. And then once we had detected that was we were being hacked, we would've to like scramble to fix it. But Rails just has this out of the box so that you can't even build forms without solving this problem first.

Cool. Any questions? Yes. So I guess every time we want to add or edit, uh, something [01:10:00] we'll need to have this authenticity token so we can just put it in the layout. This great, great question. Can we just put it in the layout? We couldn't put it in the layout because we need it to be inside the form with a name so that it shows up in our pram slash Right.

So that's a good idea. So that wouldn't quite work in the. But trust. But at the end of like the next couple of days of claps, we're going to see helper methods that Rails has that just does all of this automatically. But we're building up to it very [01:10:30] incrementally. But you have the right idea. So in the meantime, we need to include this line of code in every place.

We want to any, any request. That's a, that's not a get. So it's posta or delete. We need to have the format, the this token. Yeah. Which final from like, its not a, there's not a, so like Yes. It's a method. So that's a great question. So there's one, one of the, of the many things we're going to start to [01:11:00] learn about our view helper methods.

We saw I think one which was, suppose I have, uh, H two and I have like time now. I was sticking that right in my form. It's like, ugh, that was terrible. We were, we learned like one helper method, which was time ago in words. And then it like formats it, it's like [01:11:30] less than a minute ago, one hour ago. One week ago.

So this is an example of, it's not an instance very anymore, right? It's a method. And these are called view helper methods. And then we give them arguments sometimes. Sometimes we don't give them arguments, just like any method. So that's not a variable containing one piece of data. It's a method that's running, which means that every time I refresh this notice that that value is changing.

Cause that method change, it generates that every time, every per [01:12:00] request. And it's always unique. So these are, this is the first of many view helper methods that we're going to find or learn about. Okay. And then usually we don't want the user to see this, so we switch this to hidden rather than text, and then the form won't go through.

But if somebody tries to be syncing and inspect and copy that token or modify that token, it won't work. Rail is going to detect it and prevent that from working a whole bunch of fancy pants, math and cryptography that we don't need [01:12:30] to worry about. Okay, great. So, um,

here's, that's one improvement. Here's another improvement that I want to make to our code. We look at the routes.

We kind of built these up during app dev one we started with slash movies, and then we started [01:13:00] with the details, page slash movies, and then a dynamic route segment. We expected the ID number to appear and then we showed the details of one thing. Then we added insert movie as a way to trigger an action that creates it when we started.

actually, this was a get as well. And then eventually we evolved it to a post. But we named these pads in a way that made it really obvious to us what the [01:13:30] intention, what our intention was, right? So we've insert movie, modify movie, delete movie. We could have named these zebra, giraffe, whatever. But we chose names that revealed our intentions for what action was supposed to be destroyed, uh, triggered by these visits.

Alright? Now, in the real world, professional developers don't do this the way that we name our URLs. Shouldn't the, the path itself by convention shouldn't include [01:14:00] what we're trying to do with the resource. The path should only identify the resource that we're trying to work with. And then the http verbal over here is supposed to tell us what operation and form on it.

So get indicates reading. So that one's good, because this path doesn't say like read movie, it just says the, the, the way we identified it. Movie, movie. And the get tells us [01:14:30] our attention. This is a topic that you probably heard of, you might have come across as acronym of REST or Rest API or Arrest Hold api.

Basically that, that term is kind of squishy these days, but basically what it means is if your routes are restful, it, it means you're, you're adhering to the naming and convention that most other web developers use. That means, uh, we don't [01:15:00] use the, which cloud function is being performed in the I itself, the request method should be used to indicate which cloud function is happening.

And there's a, there's a useful link here on how to resource, how to name resources if you want to, but the gist of it is fairly simple. All of our routes are going to start with slash and then the plural version of the table name. So these are actually good. [01:15:30] And then we have a dynamic route segment with an ID number for an individual record if we want to modify it.

So I'm going to change this route here to slash movies. And here I'm going to change this to the verb patch. So now, even if, even though these two paths are the same, [01:16:00] we won't have a routing ambiguity because they have a different HTB burden. So Rails can differentiate the requests. Similarly, to delete a movie, we're going to use the HTB verb delete.

And again, this should be movies. And this should be movies. So it all starts at slash movie slash movie slash movies. And these two are not going to get mixed up again [01:16:30] because they have different verbs.

So that means if I, so with this change, if I want the form that we just fixed to work, I need to go back to the form itself, change this to slash movies. The method posts should remain. If I go back and refresh and try it again, click on create, it should work. So make sure that you update the action here to just slash [01:17:00] movies and then the route to post slash movies.

Yep. So if you manually type in the URLs, go to the first one. Uh, if you manually type it into the browser address bar, the browser's address bar can only perform get requests. So in this case, it would go to this one. So that's why that one we started out with get for Everything, so that it would be easy for us to manually type it in and [01:17:30] test it.

But now we're evolving past that. I might have missed this earlier, but I see how the verbs at the beginning, like, tell us what we're trying to do, but why is it a problem? Like you said, you should never put the action in the url. Is that like a security? Not really security? No. Like we did it have to one, and it worked and then, and once we switched it, switching to from get to post, that was the thing that we needed to do for security reasons.

After that, the way you name your [01:18:00] URLs is just up to you. It's not necessarily going to cause any problems. But this is an example of how we're just trying to like level up and learn the conventions that professional developers use. Because now, like whenever we use somebody else's API or they use our api, you can pretty much just guess what the URLs are going to be instead of having to learn what each developer decided to name each one of their routes.

Got it. Yeah. Can you go back to the, yep. So we just have to make sure that this action matches the [01:18:30] URL that we switch to.

All right. Yeah. Basic question, just to make sure. What is the difference between main name and value? Main is what's going to become the key in the perhaps hash. So when I actually submit this form, go to my server log

and clear it and submit this form, [01:19:00] look at the server log. So, In the prime. Now we have a key with the name of authenticity token and that's, we have to, we have to have exactly this name cuz with this CSM protection enabled, any time there's a post, if there isn't this key with a valid value, Rails will reject the request.

Right? So this one we don't get to set and the other one we can just whatever kind [01:19:30] of, except in this case for this specific purpose, we don't really get to pick whatever we want. We have to use this, this helper method generates that very specific string that nobody else can spoof. So we, we can, we couldn't even spoof it if we tried to, we have to use this helper method to generate it.

Okay. I think. Good. All right, let's keep going and fix the rest of our app to adhere to [01:20:00] this new name convention. So my index page is fine. My show page is fine. I didn't change those, but the delete and update changed. So if I go ahead to, so I go click on the show details here. Oh, here's another thing. I jump out.

So I clicked on the show and we get an error, error message on Define Method Act for active record relation line 27 of movies controller. Alright, here's what's going on here [01:20:30] I go to the line 27 of Louis Control. All right. So dot where searches the movie table returns an active record relation with all the matches.

Put that in his variable. And I, you have to have one. I told you all, just think of it like an array and use, use it the way that you use an array, but it's not actually an array, it's an active record relation. This method.at exists for regular, plain old ruby arrays, [01:21:00] but it actually in the real world, doesn't exist for active record relations.

We just added it to active record relations and act at one projects, just to make it more familiar for us to be accessing an element. So from now on, when you have an active record relation and you're trying to get a single element out of it, you could do square bracket syntax or you could do dot first.

These are, these methods are shared between arrays and [01:21:30] relations, but you just can't use that.app anymore. So anywhere that you're doing.at on a relation, we're going to have to switch it to dot bursts or dopa square brackets. Lemme make sure that works. Now I can get to this movie details page. Any questions about this?

the.at method, this square brackets syntax for accessing something in an array. Is by far the most common in other [01:22:00] programming languages as well. So it's not a bad idea to just start getting used to it. When you're reading other languages or when you're reading Ruby, you're going to start to see, you're going to see the spread brackets much more commonly than the.at.at is pretty much just active one for draft stuff.

Okay? Now when we click on delete, it says, okay, no wrong patches cause we used to point to delete underscore movie not [01:22:30] working anymore. So if I go check out the code for that delete link, which is in the movie's show template, line 15, I have to switch this to slash movies to match up with. What we have now is around final.

But if I, now I'm trying to use that and I click on delete movie, it just takes me right back to the routes page or the the show page [01:23:00] because this is still a get request. And if you do get movie slash ID number, that's just going to go to the details page, right? So now we have like a kind of a conflict between the two.

So we need to make this aag submit a delete request instead of a get request. Now this sadly, I wish we could just do method equals delete.

Kind of the way that we do in the form that would make a lot of [01:23:30] sense. But for some reason in HTML, they don't have delete. They only have post and get. People who wrote H M L are different than the committee who wrote HT d p, and they apparently didn't share the memo. So we only have Gap and Post, actually.

Fortunately though, Rails includes some fanciness that will let us fake this pretty easily. We add a data dash method attribute, delete, and make sure that [01:24:00] this works, and then we'll chat about it. Okay? So it works. But we have this app issue, which we can fix in the Destroy action in a second. But if you add this attribute onto a link, Rails will add some stuff in the background that makes it appear like a delete request to our server.

And then we can use this in our routes without any trouble. So make that change and then resolve this next issue, which is online. 66. Same issue with the.app. We're [01:24:30] going to go back here and do the dot first.

Now

the lead works

with. So far. Good. Any questions? Any issues? Are you stuck?

Okay. Last thing we need to fix [01:25:00] then is the, uh, update, the form to update. It's going to go down. I need to go to the show page. And so we're here. There's a form starting online, 69 to modify movie, but now we switch this to movies slash movies slash and then put the ID there. Okay. Now we're going to have the same issue [01:25:30] where we want this to place a patch request so that it goes to here and it doesn't get tripped up Anywhere else?

Patch, I wish, I wish I could just do patch, but again, HTML doesn't have that bird, so we're going to keep it as post. And what we do is we include, well first we need to include the ity token, just like we did before, [01:26:00] type equals, let's start with text value equals form. Ity. Embed that smoothie, generate the string properly.

First, we need that hidden input or I'm just keeping visible for now. Secondly, oh, have a name of just token, [01:26:30] so that will allow it through the csrm protection. Secondly,

we need, I'm going to forget this. Lemme see if I remembered it. I think it's method.

I'm going to try this first and make sure that works.

Think it worked to fix this issue[01:27:00] 

first here.

Okay, good. So here is what I added. Was this in good? The reason I don't remember, I don't memorize any of this. I have to remind myself every time I teach FDO two because we're going to get to a point where we're using advanced helper methods that generate all of this [01:27:30] automatically for us. But up until we get there, we're going to have to use this manually.

So in with the link, we're able to fake a delete request with just the data method attribute on the link itself. Performs we have to include an input that has the very specific name, underscore method, and then the value of patch in order to thank the patch request. Now we're able to have restful routes for the index, the show, [01:28:00] the update, the create, and the delete.

We're going to help you get stuck. We now have nice restful rounds. Please go back to Sure.[01:28:30] 

Underscore has no special significance. It's just the name in the PRM slash that Rails is looking for, and if it finds that, then it'll use this value to change the type of the request from a post to a patch when it's looking through Rosta RV for a match. So when I look at it [01:29:00] here in the server, when I did.

Authenticity token when we did that one, we can see that that actually showed up in the PRM slash like our other key value pairs, right? Yeah. The OnCore method one doesn't show up in the PRMs, but that's what changed the request up here from opposed into a patch. The presence of that key value pair [01:29:30] looking for literally Rails is looking in the, in the incoming parameters.

In the in requests. It's looking for a key underscore method. If I had just method that it wouldn't work cuz it'd show up just as a regular but underscore method is supposed to be a way to like make sure it doesn't complete with any actual parameter. Method is like kind a common thing. Somebody might actually make an input method so they just put underscore in front to reduce the probability of somebody accidentally using that key.[01:30:00] 

We use X and image. Uh, so for these two we pretty much always use hidden. I was just doing text so that we had something to look at. But you should use it.

Yeah. Make right now we should keep getting to the point where database, yes, that's it. And edit and everything. Everything should be back to working. So basically the goal is [01:30:30] we've switched our routes to be restful. Yeah. And now we need to make it all work together cause we broke everyth.

So,

[01:31:00] oh,

so we did three things, right? First and foremost, we switched the action to point to our new arrest. Then we have to include this in order to get through [01:31:30] the cross-site request order protection. And then we had to include this to change to kind of fake a patch request because forms don't have the ability to just say, patch, your honor.

So this is how we can make it patch with a patch in.

This is we. So yeah, we, you have to use this name. We don't get to pick Rails is going to look for specifically. [01:32:00] A parameter that has the name underscore method. And if it sees one of those, then it'll interpret. Even though actually the request is a post coming to Rails for routing purposes, Rails is like, okay, because I see this in the pram hash, we're going to interpret it as a patch when we figure out which route it hits.

Yeah. And this is sort of a, it's just best [01:32:30] practices. So we're just learning best practices now. We're becoming pros. So it's time to start using best practices, but it, it is going to pay, it seems like kind of our journey, extra work right now. Trust me. What we get to the end of this sequence, by, by next week, you're going to see that by adhering to all these injections, we're going to be able to do what we did in after one, using like 75 lines code.

It's going to come down to like 10 once we adopt all these con, but then they always compound on each other and let us shorten our code [01:33:00] line. So the, for, uh, all of these changes that we've made, we never had to, um, make, um, like sort of the parallel changes to the label tag. Oh, you're right, actually, um, well, we haven't changed.

So for these two, because they're hidden inputs, we actually didn't even put labels in. Right. Labels are for people to see and for people to click on for accessibility purposes. But since we intend to just hide these anyway, we need them, but the users never see them or know that they. [01:33:30] We don't need labels.

Now we are going to start to modify these as well eventually. And then we're going to have to update the labels to match. Like we're not going to do this today, but generally speaking we just use the name of the value here. So this is all, this is going to be titled, that's going to be titled, and this is going to be title.

We named them all different nata one to help us keep, keep it straight, what matches with what. But in a conventional code base, those are all just going to be the same thing as the column. [01:34:00] So we're going to make all those changes eventually, but not yet. Yeah. Does it matter where in the form put this input Now it doesn't matter.

I mean, generally speaking this is not, not just for these two, but for any inputs, order doesn't matter. But if you happen to have two inputs with the same name, which you shouldn't, that's a bug. But if you do, the last one is the one that will, will actually make it through the frame session. But you should never have two inputs with the same name anyway.

Almost never there's,[01:34:30] 

okay, good. Let's make two more quick changes and then we're going to take a break and then we're going to keep going. So the quick changes are in here we have path id. So this is the name that we chose for this dynamic route segment. And I made this name up path Id just because I wanted an easy way to talk about the fact.

That is something that's going to [01:35:00] appear in the browser address bar or in the request in that spot of the path so that when we see it in the PRM slash we know where it's coming from as opposed to something that's coming to us from a query strip, for example. Now in the real world, the developers just call it idn.

We can call it ID zebra or whatever, as long as we know what it is, then in the controller we use that to fetch it. It's up to us. But I just want to let you know in a real Rails code [01:35:30] base, everybody just calls this id.

So we're going to start to do that again. You have to, you have to remember yourself, that when you, when this is going to go into the PR hash and you need to fetch it, and it's coming from the url, not from the, uh, from the path and not the query string. So let's switch those to id and if it's id, then we're going to go to controller.

Wherever we have [01:36:00] path id, we need to update that to just ideally to match. You can just find and replace if you want to as well,

delete some of this stuff here. Is there a question? Yeah. That's to replace everything. So what I just did here was, uh, I selected the first instance of it. And then I get command D [01:36:30] and I kept, I hold the command and I keep pressing D or it's control D on windows. Then you get a cursor at every spot and then when you type, it repeats everywhere until you click somewhere with your mouse.

You'll have a cursor at all those places. Or you can command shit f or uh, the replace dialogue over here. And then you can find and replace and change things like all across the entire app and all the files. I just, one, if you're going to do this mass finding [01:37:00] replacer even before you do this, find and replace in a single file, usually a good idea to make a gig commit first.

Cuz I then really mess myself up big time by finding, replacing and getting it wrong. And then I'm picking through hundreds of files for the next follows. Okay, cool. So we're going to do that and I think that's good. So as long as you don't have any anymore. At zeros we have dot first or square brackets. We have [01:37:30] IDs.

Our, our, our routes now are done. They're like industrial grade. This is what a proper restful API would look like. Alright, let's pause there. The next thing we're going to do is build pages separately for, uh, add and edit instead of having them on the show page and on the next page. But let's take a break first and.[01:38:00] 

We'll get started again at 7 55.[01:38:30] 

That's

taken, but I'm pretty sure what happens.[01:39:00] 

I think U is, that link is not keep rolling. No, it just.

It just like not the expected[01:39:30] 

somewhere. I'm not sure what it'll actually read out here. You'd have to add like a text what it was doing, but just the expectation, like buttons going to perform

all the websites that I know, or News link, but they, [01:40:00] they probably, they're accessible. They probably just have a button. Like the actual underlying element is that could be true, but I doubt so I, as far as I'm just world Yeah. The world, that world that exists

conform to the world that exists. Right. And I would expect with the prevalence of like, you know, it's an amazing thing to read though, [01:40:30] um, I forget, is in one of, she has you. It's aor incredible

element, but only like you have to use a screen to listen to how, when it's focusing and that experience of even just that one little exercise. I didn't,[01:41:00] 

he already offered me a pretty solid discount for the CSS

to get, but hopefully maybe he'll bundle both of.

Do you know how much I paid? Um, I paid

it's less,[01:41:30] 

which is good.

Okay.

To refresh.[01:42:00] [01:42:30] [01:43:00] 

So[01:43:30] 

filter.

Status duct.[01:44:00] [01:44:30] [01:45:00] 

Let's say they have[01:45:30] [01:46:00] 

for the colors and everything.[01:46:30] 

Oh,

you too.[01:47:00] 

More safe than.[01:47:30] 

But that's awesome. So did you.[01:48:00] 

Also do the same thing,[01:48:30] 

and that just lets me figure out the hard parts and then I just, I don't actually give them.[01:49:00] 

Hopeful you'll be able to go a little bit further in the[01:49:30] 

say, good to see you. Um, so

up until chapter five going, well, the tests make sense

back into it. [01:50:00] Testing.

Okay. But as usual,[01:50:30] 

Yeah, I actually started the, this past week I was thinking about actually. Okay. I was like, oh man. Like yeah.

Yeah. And like you explain like I can figure out the logic.

Movies complicated. I dunno where the logic is coming from. Write yourself.

[01:51:00] Yeah, we're, that's one of the things,

you going to hit the path and go, go bus sellable. Have to

charging. So, okay. And then the other routes are io it's charging through. Oh, I [01:51:30] do that too. . I mean, depending on how much time you try, like I'll be hosting three resources in both and we'll be talking in class a little bit each day about both things. Both

slacks you, you.[01:52:00] [01:52:30] 

Integrated, there's,[01:53:00] 

it would've just after you opened it up for a little bit. The greatest, yeah. Three Wonder Canvas. Yeah,[01:53:30] 

possible should be fine for this. Um, probably an email if there's no,[01:54:00] 

I have a good sign email. What did I get?

You think great on it. Like I didn't think about this. That's the actual Okay. I'm not sure about [01:54:30] your

Oh, yeah, yeah.

Alright, everyone, we're going to get started again. You could get back. To where we were at and I realize now looking at the notes that I totally skipped a step, which was, there's a section here that says the goal [01:55:00] and I wanted to give you a preview of why we're doing all of this cuz I know it seems a little bit arbitrary right now.

Like why do we have to switch the methods and why do we have to use all that? Here's why. So if you copy this command, which is very similar, it's Rails generate. Then there's a name model and columns. But the difference is right here, the name of the generator we choose is Scaffold. This like the model generator and the controller generator are just built into Rails.

Let's take a look and [01:55:30] see what happens with this generator. We're going to it in, run it. And

unlike the `draft:resource` generator, I didn't have to add a gem to get this to run. It's just built in out of the box. It's sticking a while. It's kinda surpris. Kinda wonder whether might workspace shut. I wasn't paying [01:56:00] attention.

Is that hanging for you guys too? I got [01:56:30] it.

Well, if it worked for you, I want you to just take a second and take a, so it's going to say down here all the files that were generated by this, just take a look at. So first of all, if you, if you Rails DB migrate, do the same thing, navigate to slash books, you'll see that you have a fully functional CRUD resource just like before.

Then take a look at Routes nrb, take a look at the books controller, take a look at [01:57:00] the view templates and try and like just compare the code with what we learned how to write Nap dev one.

Um, this wouldn't override anything cause it's different[01:57:30] 

adding a second database.[01:58:00] [01:58:30] [01:59:00] 

All right, so while they're waiting for my gift pod workspace set up, which is taking a long time, what, if any differences are you puzzled by here? Yeah, there are no routes. There's no routes. But you can visit Flash books though, and it works. So the routes do exist. Let me try to do this here, see if it works this time.

Okay, cool. [01:59:30] Migrate and server, and I don't know if you remember, but there's a tool here, kind of like there's slash Gid and slash Rails db. There's another tool called slash Rails info.

My servers running slash Rails slash info. This is the path that you can always visit in development mode, and it lists out all the routes that exist [02:00:00] in Roths dot rb, and you can even search them here and filter them. So here's all the movie related ones, and if I search for a book, there are like slash get to slash books and post to slash books.

Those routes exist somehow and I'm able to visit them, oops. Books, and I can add a book.

It's [02:00:30] created and I can see it and destroy all the usual stuff. So this created a full resource for me. But if I looked around,

There's no, where is the routes? Wait there look,

it added this one line, this help, this method resources. If you give it [02:01:00] the name of the database table that you want to build a front interface around, it writes all seven routes and it writes them restfully week and it does a whole bunch of other stuff that we'll talk about. I know, right? But imagine if, and I one, like what if I introduce this on day two, like, Hey guys, right then, and that's actually how a lot of people learn Rails.

So hopefully this is a little bit easier, but by the time we get to this, you have to be able to understand that [02:01:30] it's just wrapping up all of this. And the convention in the community is to name our routes restfully and therefore that helper method generates restfully named routes given the database state, right?

So this is why we're bothering all this. What's that? I guess you'll get to question. Well, what is it? Just if I want to delete one. Right. Okay. So yeah, great point. Like a lot of times we don't want all, all of these rocks, like maybe we don't want people to delete whatever it is. You can [02:02:00] customize this here with a hash and it would be like only, and then you provide an array of the ones that you want.

Or you can say, accept. And exclude the ones that you don't want. Okay? And there's like a ton more power. Like this is where rail starts to shine actually for what we learned, app to have one, we don't actually need Rails. We could have used a much simpler and lighter weight, lighter weight framework. But when you [02:02:30] get to building industrial grade applications, Rails, the, the tens of thousands of companies like GitHub and Airbnb and Twitter who use Rails have come across every single like use case like that.

Like, oh, what if I don't need all seven? I just want six. That has been encountered and solved in the best way that these brilliant lines could think of. And we just get to take advantage of it. So one little example. Okay, so here's the routes. We go to the controllers, books controller, [02:03:00] like look at, look at the edit.

Actually look at some of these actions, like they're so short. Where's all the code? Well, once we adopt the conventional names for our actions, our view templates, our variables, and everything else, all that code that the boiler plate code that we just have to repeat and it, but it's the same for every controller.

The only thing that's changing is the name of the table [02:03:30] Rails will just, if we leave it out, like you can see here, where's the render state? How does it know what template to render? If the template is named the same thing as the action, which we usually do to make it easy for us to find an abuse folder, if the folder is named the same thing as the controller, then you don't have to say, render template books show erb.

First of all, [02:04:00] HTML ERB is a default. So we can leave that out and if this matches this, we can leave that out. And if this matches this, we can leave that out. And Rails will just try that by default before it throws the no template error. If you want to name it something else, then you have to type it all out.

And sometimes we do want to name it something else, but most of the time we don't. And therefore we can stop. We don't have to include the code. It adds cognitive [02:04:30] overhead. So for beginners, they all have no idea what's going on, but once you've built five or six apps, you're sick of typing that over and over.

It's like, okay, get it already. You can just start to leave it out. All right, so there's that and there's a whole bunch of other stuff. This whole, here's an example of where it actually added code that we didn't write. And the reason for that is this generator includes responses for multiple formats besides just H T M L.

So [02:05:00] let's suppose we're ready to add an I format to our app. Our app is taken off and it's time to. iPhone or Android apps on top. Step one is we have to split the front end and the back end and we have to have a J S O API and then our iPhone and Android app will consume the JS O api. Well, in Rails we have a book or two

back [02:05:30] Rails rather. Cool. Now we want to start to add adjacent api. Well, I implicit, whenever we've been visiting a an url, we haven't been including it, but there's a dot html on the end that if you omit Rails, just assumes you're asking for the HTML page cuz that's the most common. But you can now, Rails makes it really easy to add different formats that you respond to.

For [02:06:00] example, if I do do JS O now, so already out of the box with the scaffold generator, there's a JS O API that we can then start to pull from with our iPhone Android app. Now there's a lot more work we have to do to make it really root robust and add authentication and all bunch of other stuff, but at least it's a start.

So that's why in this case it made our code longer, but it's because we have support now [02:06:30] for json. So we'll, we'll talk about that when we get to later. All right, so. This is the point. It might seem like what we're doing for the next week or two is like arbitrary and it's like, okay, we're changing the names of routes that were already working and we're actually making the names look less understandable by changing the, the, the paths.

But the benefit is eventually we'll get to use all these shortcuts and Rails, gets to do a bunch of workforce, which speeds us up, lets us avoid typos and bugs by typing less code. And that's the main [02:07:00] benefit. So good. Okay, so let's get back to it then. One thing that we will see is on the index page of a scaffold, we don't have a form to add a new book.

Instead there's a link here and conventionally the form to add a new record to this table is located at a path that is just slash new after the [02:07:30] name of the resource that we fill it out over here. Similarly, the edit, the edit form doesn't show up right on the details page. Right. I think that's pretty rare for the edit form to be on the details page.

Typically have to click a link to get to another page that has the edit form. Okay, let's do that. We're going to update our movies to be kind of like that. I don't, I want to move this form into its own page. So let's go to, first of all, Rossby [02:08:00] and add.

Get slash movies slash new, and then controller goes to movies. Then let's make an action called let's add a new action called New,

which is the conventional name for that action. And then we have to do the same old things. Think way back, we have to connect Route controller [02:08:30] Action and creative view template. So defined slash new or a method called new

and render a template. Okay, I'm going to, let's pause for one second and I am now going to finally start to stop typing out the longest version of everything. So the way that I always did this after one was parenthesis for the arguments, [02:09:00] then a hash here, and then template here, movies, new H, right? However, we saw that there's a bunch of different styles that you can write.

Movie, this is the most explicit, but we're going to start to adopt some of the more idiomatic ways of doing it. First of all, when we have a hash, the hash is the last argument to a method. We can [02:09:30] drop the curly brackets. Around the hash. Literal the only one. It's the last argument to a method. No other time.

So if we just have a hash out here

like this, you can't just drop the curls out in space. Now it's a syntax error. But when it's the last argument to a method, which en Rails is like all the time, [02:10:00] right? With routes, with dot wear, with render Rails, methods are designed in this way where there's usually a hashes. The last thing that lets you supply a whole bunch of different options.

You can drop the curls or we're going to start doing that. The other thing we're going to start to do is when the key in the hashes a symbol as of Ruby 1.9, they added the ability to move the coal into the end and drop the hash rocket. [02:10:30] When you're typing this out a thousand times, this saves you a lot of trouble.

Sorry guys. Uh, so from now on in class two, I'm just going to start typing in hash literals out this way instead of the long way, and then unwrapping it. The last thing we can do is with methods you are allowed to drop the parentes. [02:11:00] Around the arguments. If there's no order of operations, care issues, my can mention is only when there's one method on the line.

And if the method is just being called without a receiver, so no object dot before it, which basically is render the routing methods like get, when I'm printing stuff with the puts method, I'll drop the parenthesis cuz there's nothing, there's no possible order of operations conflicts there. This is what you're [02:11:30] going to see now.

Like when you go out and start reading blog posts and stack overflow, this is the syntax that you're going to see and you just have to kind of unwind it in your head to put it back into a form that feels more familiar. Okay, so let me now try and visit slash new and we got to the right place and it says missing template.

Let's create that template

and [02:12:00] copy this form. Everything from this page two, line 13 all the way down to the closing form tag. Just copy it over Going to, um, our auto format's not working in this workspace, but we'll fix it. Um, then if I refresh this, we should have this. If I had a movie, does it work? Second [02:12:30] works. We didn't have to do anything else except just copy it over because the action still stays the same and the methods the same.

Everything else is the same. You just put it in its own page

and just test to make sure that it works. Can you check real quick with homework,

any questions on this new form? [02:13:00] If not, try to do the edit as well. I want edit forms to appear at Movies slash ID number slash edit. That's the typical location, so at a route to allow for this, and then on that page, put the edit form.[02:13:30] 

Actually copy the form to create movie, which previously was on the index pamphlet. It just moved it over and it worked. The edit form is not going to work with just copy pasting, but tried to figure out how to make it work.[02:14:00] [02:14:30] 

Um, you're just trying to, this one is just, you're just kind direct to the, to the page itself.[02:15:00] 

Oh,[02:15:30] 

basically.

Okay. Um, yeah, let's go back to their officers. [02:16:00] Um,

yeah, we creating a wheel route for edit. Yep. Okay. Want now [02:16:30] something like this to work? So, oh. Looks like you have a little spin on the, this should display a form to edit whatever.

Syntax. Do we not need to? Yeah, there we,

oh actually, well, okay. Great question. No, [02:17:00] because the purpose of this to just explain the form, it's not actually updating a database record. So we're getting the page that has to pull on Do we have to keep using the rocket or we move that? Yeah, I mean you should actually try to shorten it up so you could drop the front seats, drop the cur symbol, drop the half.

Yeah. [02:17:30] Um, can you go back?

Okay, let's go back to,

so one thing we want do is direct to Yeah. We're do something.[02:18:00] 

No, we want keep that cuz you doing two considered going to separate things. This one is just getting the age that's going to show the report and the other actions going to actually allow us create.[02:18:30] 

The concept,[02:19:00] 

we'll get to it later, but

I'm going to start to step through this. Sorry if you didn't finish yet, but we're running a little short on time, so I want to make sure we get to what you need to for the homework. I think we'll, we'll get to like, alright, so what I want is, rather than edit form being right on the details [02:19:30] page, I'd like to have a separate route that looks like this and the edit page will be there.

So I added a route movie slash id slash edit. Also, let me point out that. This get slash movie slash new. It's higher up in the routes file above get movie slash ID if you put it lower below this. Now these two are in [02:20:00] conflict. They're the same verb and slash new will count as a dynamic passing. So now this route will never be reached.

So watch out for that. If you ever have a static route that matches the same pattern as a dynamic route, make sure that it's above so it doesn't get caught at the dynamic route. Does that make sense? Otherwise, you're going to go to the show action. It's going to look for a movie with the idea of new, and then it's going to crash, saying that doesn't [02:20:30] exist, right?

So let's move this up. And we need now to do movies such ID slash edit. I made the route, let me implement the action goes, copy the new action and change that to edit and then create a new template. I just duplicated the new form

and just to get it working. [02:21:00] I have some stuff in there. Uh, I just duplicated the new page. But of course, I need this to be an edit form, which means this form should be prepopulated. With the details from movie number four so that I can just change whatever I want to change and then update. So I already have an form on the show page, so I could go copy that I'm feeling lazy, look at this, go to my edit page, [02:21:30] paste this in, say update.

And if I try this, I get an error right here because we're trying to call that ID in that form. And this instance rate well at the league doesn't exist in this action. So what we need to do is look up the movie [02:22:00] based on the brands,

just like we did in the show action. I'm just doing it all on online now. And that should then make the form work, I hope, make sure, okay, so now I have this and I think if I update, it should work. It works, the formal works as long as we supply the right instance [02:22:30] variable that that other template was using, that it should.

Does that make sense? What do you think? Yeah, the, when you're fetching from the branch, you can either put the colon in the front or you can use the same name. But quotes is that is one the bird I see fetching here. Yeah. Here I use a symbol. You also see me a lot of times using the string. Yeah. And this is after I harped on you a bunch of times saying those two are not interchangeable.

However, the prams [02:23:00] hash is some special hash Rails. It's not actually a hash, it's a subclass of hash that Rails created. And it is, it's called a hash within different access. And you can use both symbol string. Most of the time you're going to see symbols. Here we use strings in active one because if you look at the perhaps hash of the server lock, everything is actually a string keys and values.

But from now on we'll use symbols here.[02:23:30] 

Okay. Any questions about getting, moving this edit over to its own page? Edit form?

You know, typically you don't have the edit form right On the details page you have to click to get to it. Yep. I uh, if you navigate slash edit now, we should still get an error cause we don't have anything on, we do haves cuz of this, the four. And then in my [02:24:00] route I had that dynamics, the second segment is dynamic.

So that's how that got into the

Okay. One last thing. I'm not sure if we're going to have time for it, but I want to talk about the experience when I fill out the form. But like, [02:24:30] what if somebody submits a movie with a blank title? Typically we don't want to allow that. So let's look at, I'm going to take a quick look at what happens with the scaffold that I generated.

So here's the scaffold that books. Does anybody remember how, what was our tool for preventing somebody from creating a book with the blank title? Validation validations. Validations are this very [02:25:00] excellent, uh, technique. If you need a refresher, there's a chapter number 43 currently on chapters@firstchapter.com.

But basically we can go into the model, we go book model, we're going to add, uh, Valenti dates, and then we say the title or the column that we want to put a rule on. And then, so I'm using the short syntax sound, so [02:25:30] not using the curls around that, moving the column in the end. Not using the parentheses, but with this now the book model will not allow a dot saved unless there's a value in that.

So that means if I try this format right now, it didn't let it, then let it work. And check out the UI here. Error to this book from being saved. Title can't be blank and even highlighted the [02:26:00] input should be cool. So if I add another one here, let's say validates the description, I submit. Now it's like both of them.

If I hire fill one,

that one's good now, but okay, great. That's a great experience. What did we do in act one? So if I can go add these validations to the movie model, [02:26:30] and then if I try to create, just read the code here. In Act one, we sheet a new record. We take columns from the form, sign them to the columns we call in if the movie do valid, which returns true or false based on whether all the validation rules pass or not.

If it is valid, we save. We're redirecting, it's not valid. [02:27:00] We're also redirecting. The only difference is we have different notice on an alert here. So that means right now if I try to go to slash movies and you know, movie slash new, I should give myself a link to make my life a lot easier. Go here, the link to movie slash note just cause I don't want to keep typing that over and over.[02:27:30] 

And then if I leave it til both blank and I click on create, it didn't create, that's good, but it just redirected to the next page. And I don't actually know what happened here. Now we did set an alert, but we don't, we haven't displayed in this application, we didn't do anything with the notice in the alert.

Again, typically what we do is we go to the application layout file because we want those alert notice and alert to show up [02:28:00] on every page if you get redirected to that page with the notice and alert. So we would add this comment that notice an alert, some kind markup so that I try

submitted

okay. At least the value there in the alert [02:28:30] because, We used this errors dot messages dot two sentence to transform the validation failures into like a human readable blurb of text. Alright, so there's a lot of stuff there. Do you remember notice and redirects and notices? Do you remember the dot errors collection that we had on the object after we got saying that it didn't work?

Errors tell us which validations failed and then we're taking the full messages strings, [02:29:00] joining them together and display the what questions?

Adding a new book. It looked like there was bootstraps added to it and there was like, uh, it looked like a . Yeah, the css. It wasn't just a standard like times new Roman ui, right? One of the things that was generated when we did the scaffold generator was in the app style asset style sheets. [02:29:30] There's a scaffolded stop css, which has some very basic styles in there.

Now I don't love these. Usually I delete this file, but it's something to get started with. It's not actually bootstrap, it's just this very basic style sheet here. It's not very long. It's like 60 lines. Okay. So yeah, we will add bootstrap eventually. All right, so this is, this is all right. But that other, that other one, that other experience.[02:30:00] 

With books. It's so much better cuz like we come back to the same form when I fill it, when I fill out the form partially correct and then submit it. At least the part that I got right stays put as opposed to like wiping it all out and I have to fill it all out again. What if there was 30, 30 columns in this?

That would be terrible to have to do. I mean, even if it tells us when we're wrong, I don't want to [02:30:30] fill out all 30 again just to fix one of 'em. Okay? So we can dramatically improve the experience of submitting this one. Here's how it goes. This is, this is a lot of dots to connect here, but it's worth it and we're going to do it for every form from that one.

So let's figure this out. First of all, when if the movie is not valid, so here we don't want to redirect to slash movies. We should at least some slightly better [02:31:00] would be to redirect back to the page that has the form on it, right? Movie slash new. So now at least if I fail to build this out, I bring it back to the form with like a helpful message being displayed in the alert.

That's a little bit better. That's like a nice thing to do. But if I type something in one but not the other. So if I fix one of these issues, It takes me back. It tells me what the issue is now, but it wiped down the form cuz we're just rendering the whole thing from [02:31:30] scratch again. Okay. Had anybody tried to invent a solution to this problem?

So instead of wiping out all the values, I would like to show the form that has all the stuff that they just tried prepopulated and then they just have to modify one thing rather than filling out all the appeals again. What do you think? Any ideas? Yeah, [02:32:00] the values and just reapply it. Ooh, interesting.

That's great idea. So we could store all the values in a cookie.

I like that. So we could do cookies and then we can store the key and title and take this,

you don't have to type this because I'm going to show you another way in a second, but [02:32:30] I do like this, so let's make it work, right? So we're going to store all three values in the cookies, and then how would I make it sharp in the page? So let's just prove that this works. I'm going to open up my dev tools. Go get my application tab so I can look at the cookies right there.[02:33:00] 

And when I fill out this form right now, say whatever create, if it worked, didn't work, is missing with the phone because of the the checkbox. This is always annoying. I'm going to comment this time. Check boxes are always tricky. Okay, so I submitted that and now there's the description and there's the title right there.

So the values that they typed in into the form [02:33:30] are stored in the cookies. Now I have them in the cookie sash. How can I make them appear here in the input? How do I pre-populate inputs? It's attribute form. It's an attribute in the form. That's right. So I go back to my new, and then here, here's the input for title.

Remember to pre-populate, we use the value attribute just like we did up here. [02:34:00] And I'm going to use the cookie sash and get the value.

And I can do the same thing before description

now. Oh, that.

Great text area, you don't need the value because it's just the content of the element for the text area. Great. So I've got [02:34:30] this. If I change this and go a description down here, all goes well. Course. Nice. That's a good solution.

I, I've never had that suggested before. I like that. I kind of actually almost like this better than the solution that I'm going to show you. Uh, but let me show you another solution here. [02:35:00] The solution that I'm going to show you is

this variable, this movie, when I do do save, and the validations failed, as we see here, this object gains an array, which has all the things that went wrong in it. And this object already has [02:35:30] the values that the user typed. We already stored those values in the attributes of this new object that we just instantiated.

So actually, this thing has all the information that we need to draw the helpful form. However, when we redirect to a new page, redirect is the same as the user just typing the same into their address bar and we don't [02:36:00] have access to any, anything from this action. So to hold to our cap starting from the top.

And we only have, once we, once we route the user go through the routing process again, we end up, up here and we only have any instance variables or whatever is set up over here. So that means that object from the create action that had the error messages and had all the values that they typed, we don't have it up in the new action.

So I'm going to say, you know what? [02:36:30] I think rather than redirecting, I'm going to render. So I'm going to, I'm going to turn this into an instance variable.

So this is now an instance variable and I'm going to render a template just like we used to. So let's render template and then say with errors[02:37:00] 

leaving out at that hrv, because if I do Rails, we'll just assume that as the default. Okay? So I'm rendering a template, I'm going to. Call it with errors, HWB. Now, in this template I have access to instant strangles.

And so now let's see [02:37:30] what happens. I submit this form, I'm rendering a template that has the movie, it didn't get saved and the idea is still no, it's got the attributes that they typed. And that means since I have this contract, I can also do

errors messages

Ruby added. [02:38:00] So now I'm rendering a template. I've got the movie object with all the information I need to prepopulate the inputs. And I also have the errors collection that I need to draw. Nice sample, hence for the user. So the solution here, even though I love this cookie solution, we're going to comment it out

and we're just going to render a template that's dedicated to showing them the form again, but with a bunch of powerful [02:38:30] stuff. I'm going to copy the form from the new template cuz it's basically the same.

And here. Instead of cookies title, we're going to use the movie title

here. We'll use movie description and we'll deal with that checkbox in a second.[02:39:00] 

Try to, we'll submit it and kind works. So lemme try this and shape into a title create. So it's rendering the form, it's displaying the previously filled out attributes. Let me also add something at the top that will display the error messages at the [02:39:30] movie, errors

messages, that's an array. And then to make it look nice, I'm going to do a each just throw into a list. So for now

it's a little better

sign.[02:40:00] 

Switch that description. Switch that. All right. And then if I actually submit them both, hopefully now it gets happy and it goes to the other branch where it just gets added. I try adding it again. This is showing up because of the cookie, so I should delete that cookie. It's kinda confusing right now.

Method that we did.[02:40:30] 

Okay, so cool. Uh, let's think about this. We changed this branch, the SAT branch. Instead of redirecting, we're just going to do the normal thing that we do, which is render a template because we're rendering a template from this action. We have, we have access to this variable, which we switched into an instance variable, and with [02:41:00] that, we're able to do whatever we want.

The new template. It's actually, you know, it's, if you think about it, it's the thing that we've been doing forever when it comes to edit forms with an edit form. We already had an object in the database. We looked it up using the id, and then we prepopulated the whole form using value attributes and the object that we looked up out of the database table.

Very similarly here, we're using the object that we attempted to save, but failed to [02:41:30] save to prepopulate. This form here, what do you think? It's a lot of dots to connect. Can you repeat a question? Yeah. Um, I've notice that the

&lt;INAUDIBLE&gt; instead previous study. Yes. Is that addressable or is that It's a great point. That's kind of why I was saying earlier that I liked the Cookies solution, but this is because [02:42:00] the form did a post to slash movies and it was that same action that's rendering this template. Right. So it's a good observation and if there are some disadvantages to it, but we just live with it.

I don't, I don't know anybody who you could, you couldn't change the, your not, but typically we don't bother, like only very tech savvy people would even notice that. So good observation. Usually we just live with it. The benefit is we're on the same action. [02:42:30] So we have the instance variable that has all the info that we need.

Otherwise we'd have to persist it like we did with cookies. So that, that's the way to address it, I guess. Okay. So this is a very good, now here's a little hack that we're going to be using that most Rails app. Use this template that I just created, the Width Arrows template for this specific purpose of reinventing the new form.

[02:43:00] How like this is super similar. To the actual new form, right? Those two templates are almost identical. The difference is there's this errors collection here displaying at the top and there's these value attributes here attempting to prepopulate. Whereas in the new form, of course, those are all just blank.

If you want to be lazy, which Rails developers are, we actually just use the same template. [02:43:30] So I'm going to make this the new temp. I copy pasted it all over it in a new template, and here I'm just going to render the new template from the sad branch of the create action. That way, let's imagine I add a new column to the movies table.

I don't have to go change two forms. I just changed the one form in the new template. So this is nice. Now I try this again, create, [02:44:00] it's working and it's just rendering that one template. I can delete this template if I want to,

and we've just encapsulated that all here. The only issue is let's, if I just go to the top, just navigate to movie slash new. I get an error here. Undefined method errors for Hill cause online five. We're trying to call the errors on. At the movie, but when [02:44:30] I just navigate to movie slash noom for the first time, I'm going to this action.

And there's no instance variable being defined here. This is the danger that you are into Anytime you're reusing the same view template from two different actions, that view template probably depends on some instance variables. And if you're reusing that template, all the actions that are using it have to set up the same instance [02:45:00] variables that it depends upon.

So how do we solve this? While we could just go back and have the two templates that's reasonable, or a hack that Rails developers uses, we just create that. We create the variable that the template wants, just put a blank brand new movie instance in it. We don't try to.save or we don't try to do, or we don't call.save or dot valid, which means the validations don't get run.[02:45:30] 

And that means that when we render this template, now the template is happy because the instance rate exists, we can still call dot errors, but because we never call dot same or dot valid, that errors question is an empty array. So this loop never runs and nothing is displayed. And then down here over pre-populating, we can call dot title and dot description, dot whatever.

It's a valid movie object. [02:46:00] It has those methods, but it's brand new, so it's blank. And so that instance variable satisfies this new template, and when we try to submit it, the same code will work. So this is just a clever hack. We're reusing the same template from these two places, and we kind of massage the template and the action and the, in the names of the instance variables to make it possible to reuse one template from both places.[02:46:30] 

Sometimes you can't get away with that. You just gotta make two different templates. If they, if they diverge sufficiently, just make the two templates and do the two different archives and keep things simple. But for many cases, this works well. What do you think? Can you think of any questions here?

Yeah. Could, could another, uh, method be adding the, the inputs that were [02:47:00] submitted to the query string, and then have the form by default just pull from the query string? Um, the immediate thing that jumps to my mind with that solution, if we just added them all to the query string, is we run into the same problems that caused us to switch to post in the first place, which query strings have a limit on the length.

Hmm. So you can't have arbitrary long content. You can't have file uploads. You don't want sensitive information like passwords, cuz then it'll just be in person's URL when they're filling out the new form. So for [02:47:30] the same reason that we switched to post, I don't love that solution. The cooking solution was nice kind of, but that would also run into the problem of if there's a file load, cookies wouldn't work either.

So yeah. Where is the, where are the values that the user input being held? Like how did it get here? Yeah, so the, the, the flow is, so I'm going to code it slash movies for the first time. It's blank form. [02:48:00] Now, when I fill out one of these and I click create, it goes into the create action, right? So the, the form sends me here with all the info in the pr slash we instantiated a movie and then we assign all the values to the movie object.

That movie Object has values even before we save it, right? Let me show you how this works in the Rails console real [02:48:30] quick.

So if I do em post movie new and then m title equals something, and then if I look at them, that object. We've assigned the attribute to the object, even though we haven't saved it yet, we're getting ready to save it, but I can get it back out, right? So the Ruby object that's stored in M [02:49:00] has those attributes, even though it hasn't been saved into the database yet.

Now, if I try to have not saved, it's like no. And now if I do M errors, full messages, it'll tell me why. But so m, even though it hasn't been saved, it still has all the information on it, including the errors collection. So now, because we turn that into an instance variable here, [02:49:30] like any action, we can render a template and the instance variables are available to us in the In the view, right?

That's how we started doing acad in the first place. Before we got to redirect, we always had a view template and that view template had access to any instance variables defined in the action. Now, in that mute template, we can prepopulate the form and display datas collection with some nice markup around it.

Tricky. Like I said, it doesn't [02:50:00] always work, but when it works, it lets us avoid having a whole other template to display the error page. Alright,

very good. We'll leave it there for today. The last thing maybe we want to do is do the same thing for the update action and make it so that we have a nice errors collection and we, we render a template here, uh, but we don't have time to do that right now. I'll let you kind of chew on that [02:50:30] over during the week.

Uh, the homework, let me make sure I didn't get anything. One second. So we added, added, dedicated, added edit pages. We added a better validation failure, and that's it. Okay, good. So the homework, there's a video where you're going to pick off pretty much where we left off just now. There's two parts to it where you're building up the same project, [02:51:00] the starting point, the wrong canvas,

the starting point here. Okay. First of all, there's a reading where I want you to go through, and I'm sending you to the official Rails guide on testing. I'm just calling out some sections to read. Now it's going to be the first example of many where when you read this, it's going to feel like a [02:51:30] lot, maybe like a little bit over your head.

So don't get too tripped on, tripped up on understanding, feeling like you need to understand every single thing. Just read through it once. Ask questions on Piazza if you have questions, but then move on to the project, and what I want you to do is just take a stab at writing some tests using the information from these sections.

We are not writing automated tests for you anymore. I want you to get in the habit of writing your own automated tests. [02:52:00] So try it. If you can get it, that's great. If you can't get it, that's okay because there's a bunch, there's examples already in the project that you can look at and then copy, paste, and use.

But I just want you to attempt writing your own tests first and like understand where to put the file for your tests, how to run the tests. Then you can use these, and this is an especially important context to have automated tests because the whole point is we're refactoring our app dev one code and making it better [02:52:30] while keeping the functionality exactly the same.

Already today, every time I made a change, I had to like click through everything. I add a movie, delete a movie, edit a movie, click through like five or six things to make sure that I didn't break anything. Once you get bored of manually testing your app, you'll understand the value of having an automated test suite that you could just run when you're trying to improve a code base without introducing bugs into it.

Okay, so first thing to do is read through this. Don't get tripped up. Attempt to write [02:53:00] some of your own tests, but ultimately you can look at the examples that are included in the project already, the project. Is helper methods and the starting the code base that you'll start with is pretty much what we left off today.

There's one video to follow along with, and by the end, you're going to be in position Next time in class, we're going to close the gap between the code that we learned and everything that you saw on the scaffold [02:53:30] generated code. We'll be able to finish that up by next time. Alright, how you feeling? It's a lot of stuff.

This is, this is how it's going to, it's how we roll and have to have two people. Make sure to book a lot of boss hours and talk through anything that seems fuzzy and use Piazza as always. I forgot to mention that on the homepage here, there's a link to piza and a link to a Slack. You we're going to have a slack now, which we didn't have [02:54:00] app to.

One rule of thumb is if it's a quick question that nobody's going to care about tomorrow, ask it on Slack, like something if you missed a URL during class or whatever. Slack is great for that. If it's something that we might refer to in the future, or you might want to refer to in the future, ask it on Piazza so that it has a URL that we can share with each other.

All right, that's it for today. Great to see you all. I'll see you next week.[02:54:30] 