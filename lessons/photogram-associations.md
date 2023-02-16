# Photogram Associations

- Notes:

  - Un-graded, optional assignment, no tests, no `rails grade`

  - `has_many`, `belongs_to`, `scope`, `through`

  - using https://association-accessors.firstdraft.com/ (needs a video tutorial, see notes in [Refactoring MSM Again][Refactoring MSM Again]

  - Below copied from project: [https://github.com/appdev-projects/photogram-associations](https://github.com/appdev-projects/photogram-associations){:target="_blank"}


In this project, we'll re-write our association accessor methods using [ActiveRecord's powerful Association helpers](https://guides.rubyonrails.org/association_basics.html).

There are no automated tests; this is just for practice. Play around in the `rails console` as you make changes to ensure that the changes you are making are having the desired effects.

Use this tool to help plan out your new association methods:

[https://association-accessors.firstdraft.com/](https://association-accessors.firstdraft.com/)

Note that the above tool doesn't yet support Scoped Associations. As a stretch goal, [read up on them here](https://remimercier.com/scoped-active-record-associations/) and see if you can figure out how to use them to build `accepted_sent_friend_requests`, `leaders`, `feed`, and `discover`.