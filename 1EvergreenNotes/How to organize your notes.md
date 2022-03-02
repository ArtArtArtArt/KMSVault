---
status: 🌱
---

Catagorize notes based not on where they come from but on where they go to. 
Answer the question : in what context will I use them?
Try using tags for it, not folders.
Folders should be used when a specific project emerges or as stages for the flow of ideas.

# Inbox names
- 0WrittingInbox - should have idea in
- 1EvergreenNotes - notes that I want to expand. Most of random note picking comes from this folder. Try adding as many links as possible. ( What should I do with problems that are similar? How to detect it? - Using extensive tag system and always add tags you will be able to detect just by looking at the graph that some topics might be merged)
- 2Outlines - outlines which connect some evergreen notes. Should be reviewed too. If I notice that two evergreen notes come together or may be part of one outline - then create it.
 - *SPECIFIC PROJECT FOLDER* - when some group of evernotes is gathered in a project with one idea I can manifest it. I create a folder and add README file where I explain what is happening. There I link evergreen notes but mostly write big comprehensive texts out of outlines
 - ZZZ - trash bin which will be freed once per week or month? Or which is freed of a week long ideas
 - 3Research - is a folder with videos and timestamps, they usually should be referenced by some transient note. 

Also make sure that notes that you create are done in the following format : ```[](X)[linkname*](https://X)```. In this case you will have both a noraml link and a graph representation.
Also organize links like this ```[[note name|context dependant name]]```. At first context dependant name may be equal to note name but later as notes get renamed you might loose the context. 
 
For proper usage of all this follow the [[ROUTINE | routine]].

Also ```[[TODO]]``` should mark potential ways to expand the existing note. And ```#todo``` should be telling about something that should be done but is not note related.

**IDEA**
What if your vaults have a limit - for example not more then 3 in reading inbox, and not more then 5 thinhs in a Writing inbox? Same goes to TODOs - 5 max for example.

**IDEA - Review plugin**
When you are working in evergreen notes use review option to delegate working on them for some other day.

**IDEA - use queries**
Use queries in files that are meant to be containers for some idea. 

# Tag system
Should be used to determine topics.


```dataview
TABLE file.cday as CREATION_DATE, file.folder as STATE
where file.cday = date(yesterday)
```


- [ ] sample task

# Queries

```dataview
table rows.file.link as FILE
from ""
group by status
```

*****

```dataview
table rows.file.link as FILE
from ""
group by status
```
Stages of the note:
 


 
#knowledge_organisation



