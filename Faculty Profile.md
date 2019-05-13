# Experience API Faculty Profile

## Medbiquitous Learning Experience Working Group

> Licensed under Creative Commons, Attribution ( CC BY)
> Authors: David Topps, 

## Table of Contents
[Recipes](#recipes)
[Vocabulary](#vocabulary)

## <a name="recipes"></a>Recipes
Can be categorized by situation type or by activity type, or whatever makes sense in context. 
### General structure:
More than just Meetings. Applicable to a variety of online collaborative activities, such as webinars, forums. 
This could also apply to team activities that are not based on electronic tools. 
However, the focus of this Profile is on activities that are mediated electronically because this is more pertinent 
to the context in which xAPI data is likely to be gathered.

Note that certain structural objects or events are regarded as equivalent in this, for example:
* a session = a meeting = a webinar = a discussion channel = a notebook = a folder ;
* or at a lower level within these, a motion = an agenda item = a topic of conversation = a discussion thread = a document.

So for tracking activities, it is reasonable to regard a meeting as the same kind of atomic object as a webinar etc. 
For Discussion Forums, this might not be so clear and worth some discussion.

| Event/object  | Sub-object | Notes |
|:------------- |:-----|:---------------|
| session | topic |   |
| meeting | agenda item |   |
| webinar | topic |   |
| discussion channel | thread| Not all forums are set up this way |
| notebook |document| http://adlnet.gov/expapi/verbs/terminated |
| MOOC | topic | Assessment of participation & contributions has been hard. Would be good to have a way to data inform the facilitators 



>### Basics/Core Recommendations
* Most statements include an Agent with the user as the 'actor' property.
* All timestamps in statements must be compliant with ISO 8601 format. (this is part of the xAPI specification) 
* This Profile acts as an extension to the Virtual Patient Profile and was developed from it. 

### Teamwork Activity Definition includes the following:  
* Has the 'type':http://adlnet.gov/expapi/activities/simulation
* The Actor object will be defined by …. 
* The Actor object for most statements with defined verbs will be of type "Agent" and MUST contain an account object.

An example of usage in a statement:

```
{
   "timestamp": 2016-09-22T14:48:06.807818Z,
    "actor": {
         "objectType": "Agent",
        "name": <...>,
        "account": {
            "name": <user_id>
            "homePage": "http://moodle.olab.ca"
        }
    },
    "verb": {
         id :  http://w3id.org/xapi/medbiq/verbs/arrived,
         display : {
            en-US :  arrived
         }
    },
    "object": {
        "id": <node_id>,
        "definition": {
          "extensions": {
            "https://registry.tincanapi.com/xapi/extensions/nodeclass": {
              "@id": "http://moodle.olab.ca/course/710",
             }
          },
          "name": {
            "en-US": <title of the Course>
          },
          "type": "http://activitystrea.ms/schema/1.0/node"
        },
        "objectType": "Activity"
      }
    "context": {
        "registration": 37933467-d275-4e0e-ab26-e2670b2fce6d,
        "contextActivities": {
            "parent": [
                {id: <course_id>}
            ]
        }
    }
    "result": {
        "completion": true
        "score": {<score object>}
        "extensions": {
            <key>: {<counter values object>}
        }
    }
}
``` 
## <a name="statements"></a>Statements
### Verb usage:



**Initialized**  
Created the session, meeting, webinar, discussion channel
* this is done by the moderator/facilitator/administrator
* this may just be the booking

Verb IRI: http://adlnet.gov/expapi/verbs/initialized  

Includes a timestamp and identifier of the node in the scenario learning design when playing was started. 
Most scenarios will have a fixed starting node but this is not always true and is not a requirement for the statement to be true.  
Note that this may need several timestamps eg the meeting scheduled start time(SST), actual start time(AST)
* note that some participants may join a session before it is Opened, since it is the moderator/facilitator who Opens the session
* Participants may not Join a Session that has not been Initialized

Note that this is not the same as Opened

The Actor who initializes the session is commonly the moderator/facilitator who Opens the session
but it does not have to be the same person.

We recommend the use of ISO 8601 timestamps because time zones are a challenge for distributed teams

**Opened**
Started the session

Verb IRI: http://activitystrea.ms/schema/1.0/open

**Terminated**  
Session ended unexpectedly, not as scheduled

Verb IRI: http://adlnet.gov/expapi/verbs/terminated  

**Suspended**
Session was temporarily halted e.g. tea break
* The expectation is that the session will be resumed
* Not used to indicate the actual end of the meeting
* Not used to indicate that a member has left an ongoing session

Verb IRI: http://adlnet.gov/expapi/verbs/suspended  

**Resumed**  
The session was restarted after a suspension
* Not used to indicate that a member has rejoined an ongoing session

Verb IRI: http://adlnet.gov/expapi/verbs/resumed  

**Completed** 
Session ended in expected fashion, as scheduled

Verb IRI: http://adlnet.gov/expapi/verbs/completed  

**Proposed**
Putting forward a motion, agenda item, discussion thread or poll

**Seconded**
Similar to Proposed and in many contexts, has to be preceded by Proposed
* a required action for some objects eg. a motion

**Voted**
Action in support of or against a proposed motion, or in a poll
* note that motions tend to be binary choices but polls can have many different options or structural types
* note that polls may be similar to Questions in some other activities (eg. see Virtual Patient Profile)
* not the same as 'decided', which would be the cause of some future action or activity.

**Agreed**
Reached consensus over a proposed issue, agenda item or action
http://activitystrea.ms/schema/1.0/agree

**Decided**
Conclusion of a motion, poll
* we suggest that in many situations, it is better to precede this verb with a definite call to action. 
* Using 'Decided' as a way of indicating that a discussion thread or conversation has come to a conclusion is risky in many contexts

**Closed**
An agenda item or discussion thread or poll has ended
* not used to indicate the end of a session, meeting, webinar

Verb IRI: http://activitystrea.ms/schema/1.0/close

**Sidebarred**
Time spent on activity that is tangentially related to the meeting process or content
* not part of the main conversational thread

**Interrupted**
Interjected into an ongoing session activity, outwith the normal flow
* does not necessarily entail a change in topic
* is not necessarily a bad thing (eg. a webinar speaker may have given permission to participants to interrupt a topic with questions on-the-fly, or there might be a question raised in the text chat bar, while she was speaking
* note that you might need to consider how to handle timestamps with text/chat interruptions eg. the time that the interruption was posted might be different from the timestamp where it became active in the conversation or the speaker noticed it

**Assigned**
Delegated a task to a team member or participant by the team leader or moderator

Verb IRI: http://activitystrea.ms/schema/1.0/assign

**Volunteered**
Offered to undertake a task
* Is not the same as voicing or putting forwards an opinion

**Asked**
Solicited a team member to share an opinion or other contribution
Getting clarification from the moderator

Verb IRI: http://adlnet.gov/expapi/verbs/asked

**Commented**
This will be a very commonly used verb

Verb IRI: http://adlnet.gov/expapi/verbs/commented

Might also use Annotated (https://w3id.org/xapi/adb/verbs/annotated)
* it might be useful to distinguish between annotations to files/documents and comments in discussions, although there are advantages to conflating them

Might also use Posted

Verb IRI: https://w3id.org/xapi/acrossx/verbs/posted

* although this definition seems specific to discussion forums
* note that in some discussion forums, you can comment on Comments, introducing a whole new stream
* need to decide whether this constitutes the creation of a new thread or not
* at the moment, this secondary stream is being regarded as a sub-thread
* this is recursive so need to figure out how in the Object you are going to track this cascade of sub-threads

**Tagged**
Added or edited metadata for an object or file eg categories, keywords, descriptors
* Such metadata is often, but not necessarily, intended for machine use
* Not the same as Commented because metadata is often not visible as part of the regular information stream, unless specifically revealed

Verb IRI: http://activitystrea.ms/schema/1.0/tag

**Redacted**
Topic or thread or comment removed from the record post hoc by the session moderator
* we suggest that such an item be flagged as no longer visible but that it not be deleted from the system, in case it needs to be reviewed later

**Ruled**
(not sure if that is the best verb to use)
Applied a rule of order or process to get a session or topic back on track, or to bring a verbose participant thread or conversation back
* some systems might only allow this by the session facilitator/chair/moderator

**Joined**
A member has joined a session that has already been initialized by the moderator/facilitator

Verb IRI: http://activitystrea.ms/schema/1.0/join

* note that the session may not have been Opened yet since the moderator may sometimes be late in joining
* (maybe should use Accessed instead)

Verb IRI: https://w3id.org/xapi/seriousgames/verbs/accessed

**Left**
A member has left an open session

Verb IRI: http://activitystrea.ms/schema/1.0/leave

**Rejoined**
Typically used after Left
* but note that a disconnection may not be logged within the system actively as Left
* May be difficult to discriminate from Joined in many systems


**Split**
Divided into parallel activities, such as small group discussions, concurrent threads
* this is typically performed by the moderator/facilitator
* this is an intentional divergence into concurrent activities, with the intention of merging again at some point

**Forked**
A divergence into a separate activity stream, without the specific intention to Merge or regroup
* In team activities in computer programming, this could refer to forking into a different branch or version of the code; or it could refer to a discussion thread

**Merged**
From split parallel activities back to common activity
* See above note about Forked for programming

**Uploaded**
Contributed a file or other learning object to the common pool for the participants

http://activitystrea.ms/schema/1.0/send

http://activitystrea.ms/schema/1.0/submit

**Downloaded**
Collected a file or other learning object out of the common pool for the participants

Verb IRI: http://id.tincanapi.com/verb/downloaded

**Removed**
Deleted a file or other learning object from the common pool for the participants
* it might be better to flag an object as unavailable rather than truly deleting it from the object store but this decision lies with the programmers of the primary system, not the LRS activity tracking

Verb IRI: http://activitystrea.ms/schema/1.0/remove

**Shared**
Changed the file access properties to include more or less participants

Verb IRI: http://adlnet.gov/expapi/verbs/shared

* will commonly be part of the Uploaded verb
* some systems may not keep these separate

**Edited**
Make some change or addition to an Initialized file/document

Verb IRI: https://w3id.org/xapi/acrossx/verbs/edited

* this is not the same as commenting
* some systems may demand that the file/document be Opened for editing, before this can happen; others may assume that a file/document is already Opened for editing once it has been initialized

**Suggested**
Proposed a change or addition within a version control system or change tracking system
eg. Google Docs suggestions vs direct editing

**Accepted**
A Suggested change is incorporated into the file/document

Verb IRI: http://activitystrea.ms/schema/1.0/accept 

**Rejected**
A Suggested change is removed from the file/document

Verb IRI: http://activitystrea.ms/schema/1.0/reject 

**Scheduled**
Create or edit a plan or timetable for carrying out a process or procedure, giving lists of intended events and times.

**Referenced**
Cited or referred to external data or source

Verb IRI: https://w3id.org/xapi/adb/verbs/referenced




