# Blending Trunk-dev and gitops
2 hot words in software these days are gitops and trunk based development. I realized some gaps in adopting both at the same time as per prescriptions.

This a quick note describes gitops and trunkbaseddev and their quick pro/cons. But they are plenty of those out there.
More importantly, this note describes how I would adopt them at the same time.

## What is Trunk Based Development:
It's simple as it says. Develop on trunk and deploy from trunk. For the gitflow fanatics and branching addicts, meetings freeze at the utterance of developing on one single branch. But, yes, for those who have lived , branching and merging hell, this concept doesn't sound as bad (in fact , a sigh of relief).
#### Trunk Based Branching doesn't mean:

 - **Don't branch at all** - But follow principle of "*branch as late as possible, merge as soon as possible, god forbid, if your branch and trunk is moving at a fast speed, reverse merge as many times into the branch*". Ideally, when someone needs to branch, these questions deserve answers:
   1. why would you break software, which requires branch?
   2. Are there any techniques , which would allow committing on the same branch?
   3. What can one do to ship software with unfinished code?

 This is not note on trunk based development, but couple of principles below enables trunk based development:
- Immutable components
- Interface Versioning and maintaining compatibility
- Use of feature flags
These techniques somewhat answers, one of the basic why's of trunk based development, which:
- **No or minimal integration efforts** - By using these techniques, one usually follows true spirit of Continuous Integration. One has less need or less efforts to "integrate" or merge each other's code. (For those , to whom merge only means source code merge, it's not so. Integration and/or merge of 2 code bases should require test cases written for each code bases to pass, at the least unit, at best integration or end to end).
- **Ship code faster to prod** - No matter how much tested in house, real test of code is in front of end user. Not only functional test, but non-functional (perf/security) and acceptance.
- **Blue/Green, Canary deployments and rollbacks** - using feature flags, behavior of code (finished or unfinished) can be put to test very easily.

### Con of Trunk Based Dev
Trunk Based development does have a **con** as well. There is no escape of advancing parts of software at their own pace. Some do it in branches, some do it within code. By doing in code, one gets above benefits. But without proper structure and frameworks, code can get a big switch statement.

Also, note, as I mentioned above, even with Trunk based dev and use of git, it is expected to have PR branches. Ideally, PR branches should not exists more than 4 hours average.

Had to take a bit of dive into Trunk based Dev before I could make my pitch on combing gitops and trunk based dev practices.

The point I wanted to make by taking a dive, is trunk based dev, does not or should not,prescribe branches beyond PR branches. Definitely not environment based branches as gitops perhaps suggests, when it prescribes configuration to be in git (per environment?) below.

## What's gitops:

Liking the clear and crisp definition here, [here](https://www.weave.works/technologies/gitops/) are the 4 principles:
### 1.The entire system described declaratively- 
This is the one I like the most. No matter if plane strikes into towers or an asteroid destroys data centers, this principle allows (*theoretically*) to re-establish the system (software and codified infrastructure) by checkout system state from git and deploy it again. Granted there are lot of subtle assumption above, in the expectation above. e.g.
 1. All data centers are "almost" equal and
 2. not all data centers are destroyed and
 3. the undestroyed data centers are reachable etc
There are certain principles also need to be followed when describing system state:
IP address range overlap is addressed
System is not data center stateful
### 2.The canonical desired system state versioned in Git -
This is where I have a slight problem. While a good principle, I think it prescribes , git for all types of states. In my experience, statefull-ness of system lies in couple places e.g.
 1. A state based infra structure provisioning system e.g. Terraform - hence tf state files
 2. Secure and un secure configuration
Thankfully, the most core STATE of the system, Business Data , is not assumed to be in git. It's a function of a database (any kind relational or unstructured).

There is not much reservation in tf statefiles in git, except, maybe performance while using http backend , but I do have opinions on secure and unsecure configurations being stored in git. Here is my view:

 - a deployment is a combination of a static verified (tested, signed etc.) artifact, whether application bit or tf files
 - artifact is created and committed to an artifactory (stealing the sexy jfrog term, but this can be azure devops artifacts or in a containerized world , registry)
This is where CI pipeline creates a verified artifacts by Continuously Integrating code from all branches into a branch.
A CD pipeline is then responsible to promote this artifact through various environment life cycles e.g. dev, qa, staging, ephemeral etc. CD pipeline combines artifacts with secure and unsecure configuration necessary for the environment being deployed.

Given this view, configuration fed to artifact can be classified into 4 categories:

 1. Secure Configuration unchanging based on environment being deployed
 2. Secure Configuration changing based on environment being deployed
 3. UnSecure Configuration unchanging based on environment being deployed
 4. UnSecure Configuration changing based on environment being deployed

Of course, directly or indirectly, all gitops articles will indicate the secrets to be pulled from secure vault. Which is correct and provides prescription for #1 and #2 categories above.
But then it also specifies, other configuration to be committed into git (I am assuming unsecure).

This is where I find issue - By committing unsecure configs for environments into git:
 - configurations can creep into code base (or environment based branches, which is what we try to avoid with Trunk based development as mentioned earlier)
- configurations of ephermeal environments can creep into source control (which are meaningless because of the life time of ephermeal env) or
- conventions (e.g. naming convention) of ephemeral environments can creep into into  code

Ideally , all 4 configurations above should be coming from unsecure and secure config stores (e.g. AppConfig/KeyVault in Azure or ).
But if the unchanging unsecure configurations are too many, perhaps they can become part of git repo.
### 3. Approved changes that can be automatically applied to the system -
This principle usually means git PR approval. But hence lies the problem, even with gitops principle of storing secrets in secure store. What if the state of a secret changes? One changes password or some encrypted key? How will that configuration be automatically be pushed by a PR approval?

This is where I apply gitops triggers somewhat differently for configurations.

If gitops suggests "**The entire system described declaratively**" and "**Approved changes that can be automatically applied to the system**" (approval of course, whether manual approval or some automatic super automated testing gates), then CD pipeline should have 2 separate triggers with either/or condition.
Change in latest artifact (or container)
Change in configuration (secure and unsecure)

If one has to follow gitops principle of maintaining state of entire system (hence system can be reproduced with any version - of git as well secure/unsecure config store), it is important to choose a config store which maintains version history of configuration changes as well. Most modern config stores, if not all, do maintain history.
Depending the implementation CD, it is important to link code/bit artifact version with configuration versions to maintain compatibility.

## A note on use of databases and it's code
Now all of this is good. But there remains the problem with the biggest state within the system.

**Business Transaction data**

If your database is code driven (like structure is defined by code , e.g. table and schema definitions), it makes it harder to implement Blue/Green, Canary and Disaster rollback difficult, if not impossible.

God forbid, your DB is not infested with sproc and trigger code.
Coming from 20 years of SQL back ground, it me slow and steady 3 years to understand, adopt no SQL databases.
But that's a whole different conversion i.e. SQL or no SQL db.

Software agents to ensure correctness and alert on divergence -

There are plenty of ways of ensuring the environment drift and alert based on state drift. Perhaps it needs a note of it's own.