## Question

Please review the data model for the Crunchbase companies data set. The document from this collection for Facebook is attached in the handout for convenience. Documents in this collection contain several array fields including one for "milestones".

Suppose we are building a web site that will display companies data in several different views. Based on the lessons in this module and ignoring other concerns, which of the following conditions favor embedding milestones (as they are in the facebook.json example) over maintaining milestones in a separate collection. Check all that apply.


## Answer

**The number of milestones for a company rarely exceeds 10 per year**
- We explicitly learned in the videos that when the number of documents of a certain type will be "few" (10 counts as few) they can be embedded & it's unnecessary to separate them out.

**Milestones will never contain more than 15 fields** 
- Although a milestone will have <= 15 fields, there can still be millions of milestones. We cannot guarantee that this will be small enough to embed.

**An individual milestone entry will always be smaller than 16K bytes**
- An entry will be relatively small, but 1,000 KB = 1 MB so if you have 1K of these it will fill up the document. We have no clue how many there are so if there are millions of documents it would argue for another collection.

**One frequently displayed view of our data displays company details such as the "name", "founded_year", "twitter_username", etc. as well as milestines**
- Access patterns are an explicit reason in favor of embedding. If something is accessed frequently you should embed it so that you can do atomic operations on the data.

**Some of yhe milestone fields such as "stoneable_type" and "stonaeble" are frequently the same from one milestone to another** 
- This is just saying that the fields WITHIN milestones have similar values. You might separate out these stoneable fields into separate documents and link to them in the milestone documents, but this tells us nothing about embedding milestones inside company documents.

## Result

- The number of milestones for a company rarely exceeds 10 per year.
- One frequently displayed view of our data displays company details such as the "name", "founded_year", "twitter_username", etc. as well as milestines.




