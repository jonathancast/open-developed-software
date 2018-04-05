# Open-Developed Software

Open-Developed Software is open-source free software, but with a twist:
 1. Everyone who uses the software pays for it
 2. Everyone who works on the software gets paid for it

Under US copyright law (and presumably other countries, as well), there is no way to enforce (1).
However, it is possible to enforce (2).

Users should pay for software on a recurring basis, probably monthly (like any other service they use).
There are two reasons for this:

 1. Software *is* a service, like a consumer durable, that provides value for precisely as long as you use it.
 2. The value of software comes not simply from the physical capital embedded in the software's source code,
    but from the ongoing support and maintenance provided to the software by the programmers.

It is, therefore, reasonable for users to continue paying for software for as long as they want it to be maintained & updated.

Users who truly want to use an exact version of a piece of software, with no changes,
may as well be permitted to do so under GPL v3 terms,
since at that point the development cost is a sunk cost, anyway.

So, ethically, users should pay for the software they use (unless they truly never want updates to it).
The law *should* be changed to requires users of open-source software to pay the programmers for the software.
Until that happens, what can we do?

We can ensure that everyone who works on software gets paid for it.
This means refusing to work on software without pay,
but I think there are reasonable rules that can be put in place to create an incentive for users to pay.

This assumes that the software is being developed by a project.
In practice, essentially all open-source software either has a singular lead maintainer,
or has some kind of organized project caring for its development.

## Paying Programmers

Take all the money users pay
(*not* donate - these are not donations - these are payments for service!)
to the project and put it into a common development fund.

Each time a programmer with commit privileges works on the project,
bill the development fund for their time at some bill rate.

Each time you accept a PR from an outside programmer,
bill the development fund for the time that programmer spent writing the code at some bill rate.

In either case, reduce the balance of the development fund by the bill amount.

Pay the programmer from the development fund appropriately.

Get a comitment from the core programmers on the project not to work unless there is enough money in the development fund to pay them.

Likewise, do not accept PRs from outside programmers until there is enough money in the development fund to pay for them.

You probably want to have some kind of margin,
where you bill the development fund *more* than you pay the programmer,
and take the extra money for project expenses.
I would use a 2x margin, so if a programmer gets paid $60/hr, the development fund gets billed $120/hr.
This allows any project successful enough to pay a full-time programmer to also pay a marketer and a salesman,
two roles which are very under-filled on existing open-source projects.

It is *very important* to put *all* the money that comes in into the development fund,
and reduce the development fund strictly in-step with actual development work,
since it helps to reinforce the idea that users are *paying* for development - these are not donations!

You want to have the same bill rate for committers, core programmers, and outside programmers, obviously.
You probably want to have the same margin for all programmers, too.
However, I think it's fair to vary the pay rate based on experience.
I would pay $30/hr for beginning programmers (no experience), and increase pay by $3/hr per year up to a max of $60/hr.

## Deciding what to work on

He who pays the piper calls the tune.

The other incentive you can create for users to pay for the software is to give them control over what gets worked on.

I would divide development work into four categories:
  1. Features / user stories
  2. Bugs / security holes
  3. Re-factoring / technical debt
  4. Support

### Features

Features are self-explanatory: they are new things the user wants to be able to do.
*Never* turn down a feature request from a user outright, unless it's unethical to do (e.g., DRM)
(but see below on program architecture).

### Bugs

Bugs and security holes are also self-explanatory.
*Eventually*, you want to patch all security holes and fix all bugs,
subject to the constraint on overall development speed mentioned above,
but you want to let users define the priority of which bugs are worked on first.
I don't believe in 0 bugs, but if you do, obviously skip this part.

### Re-factoring

Re-factoring and technical debt, for the purpose of this document, is defined as development work whose benefit acrues to the programmers.
This is important: it makes future features and bug fixes cheaper to write for the users,
and makes it easier for you to keep programmers and attract new ones.
But you do *not* let users prioritize this category;
let programmers do this independently and just bill it to the development fund automatically.
What you can do is to provide a guarantee about how development time will be split up among the categories,
e.g., at least 50% of development time on new features, or no more than 30% of development time on re-factoring,
and stick to that.

I am *not* a big fan of agile approaches like including re-factoring time in user story estimates,
simply because I *don't* think it's honest to the user,
and this whole approach is about strict integrity.
If a feature requires 3 days of re-factoring and 1 hour of development time, be honest about that.
If a feature requires 3 days of re-factoring and 1 hour of development time, or 6 hours of development time, be honest about that, too.

But always write this software the best way.
If the user knew how to write software, they would be writing it themselves, right?

### Support

Support, for the purposes of this document, is 'optional' development that's specific to a particular category of users.

Examples would be:
  * Porting the software to a new version of an OS.
  * Fixing platform-specific bugs.
  * Keeping the software working on an old version of an OS while moving it forward in other ways.
  * Keeping an existing feature / workflow working during architecture changes.
  * Back-porting bugfixes to older 'stable' releases.

I wouldn't prioritize these, or ask users to prioritize them.
Instead, ask users to check off which OSs / features / stable version, etc., they use;
then officially drop support for items where the % of development effort going to maintain them is substantially larger than the % of money coming in from users who actually use them.

### Voting

This applies to features and bugs.

Pick a 'standard' amount of money you expect users to pay for the software;
each user who pays that amount gets one vote.

In some cases (system software), it makes sense to give users more votes based on the number of downstream users they have.
But in no case should a user get more votes than they pay for,
in no case should someone who doesn't actually use the software get a vote (although policing that may not be a huge deal for your specific case).
I don't think it's a good idea to just let people pay extra and get extra votes, either;
you want some kind of one person - one vote rule, for fairness.

This is a modified form of the proportional voting scheme used in Europe, although it may not look like it.
However, it's much fairer and more democratic, because there are no party lists.

Have each user provide a list of the features they want worked, from top to bottom (#1 to #however many they want).
Same for bugs.

I do not recommend combining the lists, which is asking users to prioritize features against bugs.
Instead, the project should decide how much time to spend on new features vs. bugs, and users should prioritize them separately.

For each story / bug, count up:
  1. The number of (votes held by) users who rank the story #1.
  2. The number of (votes held by) users who rank the story <=#2 (#1 or #2), divided by 2.
  3. The number of (votes held by) users who rank the story <=#3 (#1, #2, or #3), divided by 3.
etc.

Find the largest quotient for each story / bug, then rank the stories / bugs by decreasing largest quotient.

## Doing Software Development

### Roles

There are a couple of key *technical* roles you want to fill.
If you have enough money, as a project, to hire 'software development managers', etc.,
just remember that *none of these roles is a management role* - these are *programmer* roles.
It may make sense to give one person multiple roles,
or to give the same person both a management role and a programmer role;
just make sure whoever you give the job to is doing *all* their roles (including management roles, if appropriate)
and don't be afraid to split roles up and give them to different people if you need to.

1. Designer - this is the person who decides how your product is going to work and look to the user.
2. Architect - this is the person who decides how your product is organized internally, and what internal components will have what jobs.
3. Programming Lead - this is the person who organizes the software development process, and makes sure there are programmers working on 
3. Lead Programmer - this is not actually a 'leadership' role.
   I would use this role to recognize your best contributor(s), without feeling the need to promote them out of development positions.
4. Senior Programmer - this is also not a 'leadership' role.
   I would use this role to recognize experienced programmers.
   If these programmers can mentor junior programmers, that's great!  Just don't count on it.
5. Manager - this is not a technical role.
   This person makes 0 technical decisions.

The designer, architect, programming lead, and any product managers / product owners / other managers
should be employees of the project,
whether they get paid a separate salary for their role or not,
and the project should be free to fire them at any time if they fail to perform.
After being fired from those roles,
they are free to continue to submit code to the project (and do not lose any committer / core programmer status they already have),
but the powers they got from those positions are gone.

### Software Architecture

Your software should be modular internally,
and should be programmable.
That means that either the software should be callable from other programs,
or it should support a plugin mechanism for the user to customize it.
Either way, every feature that is accessible to interactive use should also be accessible to scripted use.
(Some 'stories', such as EME / DRM, may try to negate these features.
*Those* user stories you can reject out of hand.)

What you are building is *not* a single component, but a system that can meet the user's needs.
A user story may come in that is not suited to any component you have currently;
in that case, it is really a user story asking for a new component to be written with new features.

A consequence of this is that an open-developed software project cannot be too small in scale.

#### Examples

 * You are maintaining a program called `cat`, which concatenates files, and a request comes in asking for non-printable characters in the file to be replaced with backlash escapes.
 
   * Bad response: add a `-v` option to `cat`.
     This is bad because `cat`'s job is to concatenate files, not to display them;
     and because it makes `cat` substantially slower.
   
   * Bad response: reject the user story.
     This is bad because the user (*who is paying you*, remember) has a legitimate need,
     and you aren't filling it.
     
   * Good response: accept the user story,
     but implement it by writing a separate program `pr` that displays files,
     and adding an option to that to make non-printing characters 'visible'.
   
   * Better response: apply these principles to the OS as a whole,
     and treat `cat` and `pr` as two components of the whole system.

### Stories

A user story is the same thing as a feature request.

A user story has the form 'As a <kind of user>, I want to <thing the user can do>'.
*Never reject a user story*, unless the <thing the user can do> is severely unethical / immoral / illegal / whatever.
Your job is to figure out a way the user can do that.
That *can* include recommending other pieces of software, as long as those work with the user's use case.

Attach to each user story a field each user voting for a story can fill out for 'in order to <value the user gets>'.
This may be different for each user.

For stories, you want to work strictly in the final ranking order.
The reason being that a story *can* be deterministically worked, from top to bottom, and finished.

Have your programmers periodically go through the top few stories in the ranking and assign a number of Story Points to each story.
A Story Point is a mythical unit of development time.
Generally, a story with 0 Story Points should be already implemented by the software,
a story with 13 Story Points should be at the upper limit of what is feasible in a single story,
and a story with 100 Story Points should be at the upper limit of waht is feasible in a single quarter of development.
The estimate given by each programmer is just that programmer's opinion,
and there should be no penalties or rewards attached to the value given.
Each story should be estimated by throwing out the top and bottom 20% of the estimates, and taking the median of the rest;
or, if you have fewer than 5 estimates on the story, throwing out the top and bottom estimates and taking the median;
or, if you have fewer than 3 estimates on the story, taking the mean of the estimates you have.

If the story at the top of the ranking order doesn't have any estimate at all, your programmers are not estimating frequently enough.

Your programming lead should periodically look at the top few stories in priority order,
and check for stories with more than, say, 10 Story Points.
He should either get clarification from the user on the requirements,
or work with the user and the designer / product manager / product owner / etc. (whatever you have)
to reduce requirements on that story (possibly adding more stories to the queue, with dependencies on the existing story)
until your programmers agree that the story should be estimated at less than 10 Story Points.
*Important*: at no point in this process should the programmers be pressured to change their estimates.
Fire any programming lead who cannot comply with that requirement.

A story should only move through the rest of this process once it has been reduced to less than 10 Story Points.
As more details emerge about a story through the rest of the work process,
programmers may raise their estimates on it;
but, if a story's estimate rises above 10 points, the programming lead should go back and whittle it down
until it falls under 10 Story Points again.

Your designer, and product manager / product owner / etc. if you have one,
should work with the users who've voted for the stories at the top of the priority list,
to understand and document (in documents attached to the story) what the user wants out of the story.

Once the user requirements are clearing defined on the top few stories,
the designer should then define an exact spec (preferably including an automated test)
for the behavior your software should have in the story.

The story should then be marked as 'design-complete'.

The architect should periodically review the top few stories, once they are design-complete.
For each story, he should create 0 or more technical tasks assigned to specific components.
These technical tasks should have their own acceptance tests,
and should explain to the programmer who is writing them how to accomplish to goals of the story within the context of the overall system.
The architect's job here is to exhibit good design sense and make sure that the story is implemented in a way that furthers the maintainability of the software.
A story would only receive 0 technical tasks when the software already does whatever the user is asking for.
(This is not a reason to reject a story, but rather to inform the user of what the software already does,
and maybe improve documentation - which is a technical task).

Technical tasks are not 'subtasks' of a story;
they are separate tickets that track the programming work used to implement a story.

Once the architect has fully ticketed a story, he should mark it 'architect-complete'.

The programming lead should periodically review the top few stories,
making sure the designer and architect are moving them through the process appropriately.
When necessary, the programming lead should select the highest-priority 'architect-complete' story,
and move it to 'in progress' status.

Technical tasks related to stories are in one of four states:
 * Waiting - created by the architect but not approved by the programming lead;
 * TODO - approved by the programming lead but not grabbed by a programmer;
 * In Progress - grabbed by a programmer but not done;
 * Done - finished by a programmer and with all passing tests, manual QA, etc.

The programming lead should periodically look for Waiting tickets attached to user stories in the In Progress status,
and move the technical tasks to the TODO status,
until the total amount of work represented by the TODO and In Progress tickets rises to the level of what the project can finance out of the development fund.

Programmers should never be paid for feature work that wasn't on technical tasks approved by the programming lead.

The programmers on the project (and any external programmers who want to help) should periodically look for TODO ticket technical tasks,
assign those tasks to themselves, and work them as normal.

The programming lead should monitor the tickets in the TODO status,
and look for programmers to volunteer to do tickets that spend too long in that status.
Under no circumstances should the programming lead assign tickets to programmers;
his job is to find programmers willing to volunteer for them.
Remember that programmers who complete technical tasks will be paid for their time.

Once all the technical tasks associated to a story are done,
and the users are satisfied that the new version of the software does what they want,
the story should be closed.
If the users want further changes, beyond what was originally included in a story, after seeing the final version,
those should be submitted as new stories and prioritized appropriately.

### Bugs

For bugs, you just want an overall priority order, with more time going to figuring out higher-level bugs.
The reason is that committing a specific programmer to work on a specific bug could just result in that programmer spinning his wheels and accomplishing nothing.
It's better to have many programmers devote a little bit of time now and then to top-priority bugs,
until somebody figures it out.
Remember Linus's law here.

The programmers on the project should periodically look at the top few bugs,
and investigate / debug the software to try to find what the cause is.
The result of their investigation, whatever it is, should be documented and attached to the bug ticket.
Programmers who find the root cause of bugs, and develop theories about how to fix them,
should create new technical tasks for the fixes,
and attach them to the bug tickets.
The fixes should then be assigned to programmers and worked like any other code change.
Obviously, the programmer who creates a bug fix ticket can also grab it,
or leave it for another programmer to volunteer to actually implement.

### Re-factoring

Ideally, the software should have a design document.
Failing that, the architect should be prepared to explain to programmers what the design of the system is,
and what it should be.
Individual programmers, or the architect, can then create technical tasks to shape the system and move it closer to the ideal design.
The architect should approve any re-factoring, at least at a high level.

Re-factoring work is legitimate work, since it makes the software easier to maintain and lowers future development costs.
The project should decide what % of time will be spent on re-factoring,
and then be un-apologetic about spending that time.
Under no circumstances should re-factoring ever be prioritized against feature development, bug fixes, or support.

The highest priority re-factorings are those that will be immediately helpful to high-priority stories or bug fixes,
or will help with high-priority support work.

The next-highest priority work is re-factorings that fix what the architect considers major flaws in the design of the system.

While you don't want your programmers spending too much time on re-factoring,
always keep in mind that it *is* useful work,
you *can* legitimately bill your users for it,
and a programmer who doesn't have anything else to work on *can* usefully spend time re-factoring.
"When you have nothing else to do, sweep the floor" applies here.
*However*, re-factoring is not just 'when you have nothing else to do' work;
it's important work that the programming lead needs to put priority on.

### Support

Support work, as defined above, should be done in special support-work technical tasks.
The reason is to make it easier to track the time spent on it,
and make sure that support work truly isn't eating up programming time that could go to more important areas.

Some support work, such as porting the software to new OS versions, language versions, etc.,
will come in as new technical tasks specifically made for that purpose;
other work, such as back-porting bug fixes, will be created as a spin-off of other tasks;
other work, such as keeping old features / behaviors working,
will be done alongside other technical tasks.
However, even in that case, it is important to create new technical tasks for the support aspect,
and track how much time is really spent on it,
so you have public documentation of what the feature really costs.

## Credits

Many of these ideas did not originate with me.
Martin Fowler, Kent Beck, and many others whose names I forget inspired many of the thoughts on estimation and implementation found here.
I do not want *credit* for any of the ideas in this document;
I want programmers to follow these practices and create awesome collaboratively-developed open-source products.
