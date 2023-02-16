# Planning Your Idea

- Notes:

  - Copied from [`planning-your-idea.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/planning-your-idea.md){:target="_blank"}

The aim of this exercise is to plan out an idea to build so that we can start to domain model, i.e., plan out our tables and columns.

If you think you're already ready to do that, then you can skip to the next article, [Diagramming Your Domain Model](https://chapters.firstdraft.com/chapters/782). Otherwise, read on.

## Coming up with an idea

If you have some ideas already, you can skip to the next section, [Sketches](#sketches). Otherwise, read on.

### Pain Points

You should think of a couple of pain points in your life that you would like to solve with a simple CRUD app. Remember,

> The verb you want to be using with respect to startup ideas is not "think up" but "notice."
> — [Paul Graham, "How to Get Startup Ideas"](http://paulgraham.com/startupideas.html){:target="_blank"}

Don't try to think up billion dollar startup ideas; our goal here is to discover a good first learning project, not to change the world just yet. Try to notice a real annoyance at work or at home or with friends that we can solve, even if for just one user — you.

For example, [here is a project that a student made last quarter](https://www.youtube.com/watch?v=U5fdaaZWwaY&feature=youtu.be){:target="_blank"} — a simple app that lets you keep track of whether or not it's time to dry clean pieces of clothing. Another student made a nice app that suggests which of your credit cards to use in order to maximize rewards based on what kind of purchase you are about to make.

If you want to get fancier than a simple CRUD app and incorporate some APIs to pull in external data, you are more than welcome to, but try to do some research[^1] and make sure that an API exists for what you want (e.g., live sports scores).

**The bottomline: keep it simple.** It's best to think up more than one idea if you can, so that we have options to choose from.

## Sketches

Once I have an idea in mind, I immediately reach for pen and paper and start sketching. If you have your own process for wireframing, feel free to skip to the next section, [User Stories](#user-stories). Otherwise, read on.

### Speedy Eights

I like to start with some [Speedy Eights](https://thoughtbot.com/playbook/validation/design-thinking-exercises/speedy-eights){:target="_blank"} to force myself to just get some thoughts down on paper.
 
I will usually do two or three rounds. One round, I'll use the 8 panels to progress through the different screens of a flow. Another round, I'll use the 8 panels to explore 8 different takes on the most important screen in the app.
   
Remember, you are only supposed to spend around 40 seconds per panel! Actually set a timer and stick to it. Try [using a sharpie rather than a pen](https://signalvnoise.com/posts/1788-oldie-but-goodie-sketching-with-a-sharpie){:target="_blank"} to prevent yourself from getting into too much detail in this phase.

### Wireframe

Then, I select one flow that I like, and I  draw out each screen in a bit more detail. I like the [Prototyping On Paper](https://marvelapp.com/pop/){:target="_blank"} app to connect the sketches of each screen together, and eventually I try to "crawl" from every link and button in each screen to every other screen until I've drawn out the entire app (excluding obvious things like edit profile forms).

## User Stories

Next, I like to create a [Trello](https://trello.com/){:target="_blank"} or some other [kanban](https://thoughtbot.com/blog/how-we-use-trello-for-product-development){:target="_blank"} board to list out all of the features that I've identified in my wireframe.
 
For the time being, I create two columns in the board: "Ideas" and "1st draft".
 
In the Ideas column, add a card for every feature that you can see in your wireframe. When I'm writing down a feature, I usually phrase it as a [User Story](http://www.romanpichler.com/blog/10-tips-writing-good-user-stories/){:target="_blank"}. User stories are just features, phrased in a particular manner:

"As a **[role]**, I want to be able to **[capability]**," (and, optionally), "so that **[benefit]**."

The aim is to always be thinking from a user-centric perspective, and not from a technology or implementation perspective yet.

First, brain-dump all the features you can possibly imagine as user stories.

**Then, re-order them by priority.** In Trello, you can drag-and-drop the cards to re-order them.

Then, crucially, ask yourself: **what is the absolute minimum featureset I can get away with in this first experimental prototype?** The prototype's purpose is just to validate whether or not the idea is feasible and whether the core value is actually valuable. **Be ruthless in eliminating all non-essential user stories for this 1st draft.**

Move **only the essential stories** to the 1st draft column.

Now that we've planned out what we want to build, it's time to [diagram an Idea in firstdraft](https://chapters.firstdraft.com/chapters/782).


[^1]: Here's a directory of [Public APIs](https://public-apis.io/){:target="_blank"}.
