---
icon: elementor
---

# Question-Set-Sections

Three types of hierarchy possible for Question sets

| **Hybrid question set hierarchy**                                                                                                                   | **Only questions** | **First sections and only then questions** |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ | ------------------------------------------ |
| <p>Question Set [Shuffle, Show x/y, Timer, Submit required, Max attempts, Show/hide Feedback, Soln, Hints, Summary]</p><ul><li>Question 1</li></ul> |                    |                                            |

* Section 1 \\\[Shuffle, Show x/y, Timer, Submit required, Max attempts, Show/hide Feedback, Soln, Hints, Summary]
  * Question 1
  * Question 2
* Section 2
* ..

\| Question set \\\[Shuffle, Show x/y, Timer, Submit required, Max attempts, Show/hide Feedback, Soln, Hints, Summary]

* Question 1
* Question 2
* ..

\| Question set \\\[Shuffle, Show x/y, Timer, Submit required, Max attempts, Show/hide Feedback, Soln, Hints, Summary]

*
* Section 1 \\\[Shuffle, Show x/y, Timer, Submit required, Max attempts, Show/hide Feedback, Soln, Hints, Summary]
  * Question 1
  * Question 2
  * ..
* Section 2
  * Question 1
  * Question 2
  * ..
* ..

|

#### **Here's the challenge** :

1. Let's say, as an example, User configures Shuffle at parent level which contains multiple sections - what does the player shuffle? Sections or Questions within section?
2.  User ends up creating sections and questions at the same level of hierarchy - say level 1 - and configures behaviour at root. What does that behaviour apply to?

    On these lines we need to think of a design for all configurable behaviour: Shuffle, Show x/y, Timer, Submit req, Max attempts, Show/hide feedback, etc..

While some of this can be exposed only for parent question set - many of these might be required at section level and will end up conflicting with parent level config. How do we handle such scenario?

What restrictions should we put in editor such that player has a simpler and robust implementation?

How do these restrictions become part of design so even adopters cannot break them by configuring otherwise?

#### **Key questions** :

1. What should be hierarchy structure? Only question, Only sections (and then questions under them), or Hybrid questions & sections
2. How many levels can hierarchy support? At present 1?
3. Which configuration to be allowed at which level of hierarchy? How to deal with overlapping / connected configurations?

#### **Possible solutions** :

**Allow people to create either sections or questions, but not a mix of both.** There should be a notion of “valid” question set hierarchy. This should also be generalised, externalised, etc.

Here are possible approaches to it..

1. Build a validator in API. By default, for every update call, validation is ON. Adopter can make an API call with validation OFF. BUT this will be a blocker since backend team won’t have bandwidth to pick this up..
2. Build a validator plugin as part of editor. Hierarchy validator. The rules for validator can be stored locally in it or somewhere in an API. This would still be easy since backend team only needs to provide storage and front-end build the logical validator. Adopter can turn off this plugin while launching the editor.

**Additional questions (mostly for Consumption):**

1. Should every section have Submit? If so, will user not be allowed to change their response after submitting a section
2. Should user see a section list when playing?
3. Should user be able to jump between sections using the progress bar?
4. For more than one level of sections, should progress bar rather become question map?

***

\[\[category.storage-team]] \[\[category.confluence]]
