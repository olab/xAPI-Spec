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



**Experienced**  
User has read a document, page or paragraph. Similar to ‘interacted’ but used when the media is static or non-interactive  
Verb IRI: http://adlnet.gov/expapi/verbs/experienced  

**Responded**  
User has responded to a question. Response to an item or question within a node, without moving off that node. (This is not quite the same as ‘answered’ which implies that the answer is correct.)  
Verb IRI: http://adlnet.gov/expapi/verbs/responded  

**Interacted**  
User has interacted with or manipulated an object or a video or similar multimedia that provides some sort of interactivity. Similar to 'experienced' for when the media is dynamic, like a video. For more detailed reporting on videos, we instead recommend the use of the Video Recipe: http://id.tincanapi.com/recipe/video/base/1  
Verb IRI: http://adlnet.gov/expapi/verbs/interacted  

**Commented**  
User has contributed to group activity. Used when an actor adds to a group activity for a compound effect. In some ways, this is not different from ‘responded’. But the net effect is different because you are not expecting that the single activity will necessarily produce some result by itself. The object might be a discussion thread. (Or in OpenLabyrinth, we have a question format called a Cumulative Question, where users contribute phrases to a single question/database field.)  
Verb IRI: http://adlnet.gov/expapi/verbs/commented 

**Ignored**  
User has ignored a flag or other scenario data. This is a flag or action sent by either a facilitator or the player engine to indicate that an action was expected by this point in time and had not occurred. Sometimes this is a good thing, and while absent, is not necessarily a negative aspect - for example, if there is a distractor in place that the actor is supposed to ignore as irrelevant.
Verb: http://w3id.org/xapi/medbiq/verbs/ignored 


For the following activity statements, the Actor is more likely to be the player engine or an object within that player engine:  

**Updated**  
Player engine has changed a counter value. This may be triggered by arrival at a particular node, or by a rule within the case design created by the scenario author, or by a timer expiration point. Although the counter value may be regarded as a score, note that the ADL verb ‘scored’ is overall score for the case or exam (http://adlnet.gov/expapi/verbs/scored), which is not the same thing.  
Verb: http://w3id.org/xapi/medbiq/verbs/updated  

**Launched**  
Player engine has initiated an action such as redirecting the user to a new node, or triggered some other activity. This is not an action made by the user.  

Verb IRI: http://adlnet.gov/expapi/verbs/launched  

**Shared**  
User has made a key resource or piece of information available to team members within a scenario activity stream.   

Verb IRI: http://adlnet.gov/expapi/verbs/shared 

Includes a timestamp and identifier of the node in the scenario learning design when triage step was started.   


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


