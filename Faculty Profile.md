# Experience API Faculty Profile

## Medbiquitous Learning Experience Working Group

> Licensed under Creative Commons, Attribution ( CC BY)
> Authors: David Topps, Corey Wirun

## Table of Contents
[Recipes](#recipes)
[Vocabulary](#vocabulary)

## <a name="recipes"></a>Recipes
Can be categorized by situation type or by activity type, or whatever makes sense in context. 
### General structure:
The focus of this Profile is on faculty member activities that are mediated electronically because this is more pertinent 
to the context in which xAPI data is likely to be gathered.

Use Case
This is for tracking the typical activities that faculty members (not faculties per se) engage in and that might be reported in their annual report, CV. Could also be used by Med Ed Research Centre Directors to provide reporting on their activities. 


>### Basics/Core Recommendations
* Most statements include an Agent with the user as the 'actor' property.
* All timestamps in statements must be compliant with ISO 8601 format. (this is part of the xAPI specification) 
* This Profile acts as an extension to the Virtual Patient Profile and was developed from it. 

### Activity Definition includes the following:  
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

**Published**  
Not just journal articles. Any scholarly output that is made available to a group via a publication or distribution mechanism
This includes scholarly materials that are needed but not made public e.g. Exams or questions or cases that are kept within a private repository. While the content may be kept private, it is recommended that for validation purposes, the activity metadata is made available for scrutiny

Verb IRI: http://adlnet.gov/expapi/verbs/terminated  

**Granted**
Activities relating to a Grant
* Applied for
* Received
* Reviewed
Generally relates to Grant work but the past tense of ‘Granted’ tends to imply that you were successful

Verb IRI: http://adlnet.gov/expapi/verbs/suspended  

**Presented**  
Suggests a live action component. Does not need to be face-to-face. Can be online or broadcast
* Includes seminars, webinars, keynotes, conference oral presentations, posters
* Context, audience etc could be specified within the Object clause, or within the associated Activity Resource Profile

Verb IRI: http://adlnet.gov/expapi/verbs/resumed  

**Patented** 
Activities relating to a Patent
* Applied for
* Received
High enough value for its own verb

Verb IRI: http://adlnet.gov/expapi/verbs/completed  

**Awarded**
Activities relating to an award and honours
* Received an award
* Distinguish from Granted
* Applied for an award
* Nominated for an award

