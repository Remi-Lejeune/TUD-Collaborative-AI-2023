## Action Trust interaction documenation

*What this document is* An explantaion for how trust is used inside ActionsTrustAgend, to understand the differences

Action trust conforms to the followig idea: The "standard behavior" of the provided agent is very human dependent. 
This is a good thing when the human is trustworthy. False information, and waiting endlessly for a human who does not come
is bound to lead to suboptimal results. Despite this, agent and human need to work together.
When in low trust mode, the agent will attempt to do as many tasks independently. Tasks which require human will be delegate to last'
Human will be sent messages.

A couple changes:

Human saying they have visited somewhere will no longer be considered 
The mildly injured and the simple obstacles will be acted on
Human will no longer override the contols.
This is for low trust (-0.5 and lower)

### Trust Impact on Message Interpreation
Trust Belief is used to 


### No Trust
Human does not override current objective
Human information is not considered valid
Human is waited for on timer

Big changes are:
Message interpratation
Action

### Little trust
Human is waited for longer
TO be developped
### Trust
Positive values