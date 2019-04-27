# Experience API Teamwork Profile

## Medbiquitous Learning Experience Working Group

> Licensed under Creative Commons, Attribution ( CC BY)
> Authors: David Topps, Ellen Meiselman, Valerie Strothers

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


## Activities 
To be used mainly if there are very specific activities being described by this profile. Otherwise, Activity types usually used instead.

## <a name="vocabulary"></a>Vocabulary

| Name  | Kind | IRI |
|:------------- |:-----|:---------------|
| Initialized |Verb| http://adlnet.gov/expapi/verbs/initialized |
| Completed |Verb| http://adlnet.gov/expapi/verbs/completed |
| Suspended |Verb| http://adlnet.gov/expapi/verbs/suspended |
| Resumed |Verb| http://adlnet.gov/expapi/verbs/resumed |
| Terminated |Verb| http://adlnet.gov/expapi/verbs/terminated |
| Arrived |Verb| http://w3id.org/xapi/medbiq/verbs/arrived |
| Experienced |Verb| http://adlnet.gov/expapi/verbs/experienced |
| Responded |Verb| http://adlnet.gov/expapi/verbs/responded |
| Interacted |Verb| http://adlnet.gov/expapi/verbs/interacted |
| Commented |Verb| http://adlnet.gov/expapi/verbs/commented |
| Ignored |Verb| http://w3id.org/xapi/medbiq/verbs/ignored |
| Updated |Verb| http://w3id.org/xapi/medbiq/verbs/updated |
| Launched |Verb| http://adlnet.gov/expapi/verbs/launched |
| Virtual Patient |Activity Type | http://adlnet.gov/expapi/activities/simulation |


