# Scenarios

This page describes the vision of how the proposed league management software will be used. It covers the following:

- High level management tasks (as performed by league staff)
- League participant responsibilities and expectations
- League event creation, progression, and conclusion
- League moderation and disciplinary actions

The duties above will be performed by various actors. They will be broken down into individual responsibilities and stories for how they will be completed

## Software usages

### League management tasks

**League creation**

- League staff create a logical league instance within the application. This instance provides a hub for league activity to reflect the events within the league.
- The hub has a unique identifier that clients can use to specify which league the event in question affects

**League maintenance**

- League staff are responsible for maintaining the integrity of the league state with given events
  - Participant and staff can submit events to change the state of the league within the application
  - Staff verify that the event is accurate and either approve its changes or deny the events from applying
- League states are traceable, so accidental event approval should be easily undone to restore to a desired state

### Participant responsibilities

**Registration**

- Participants can register to participant in a league using the registration interface
- This creates a registration event that must be approved by league staff before registration is finalized
- Registration must be finalized before the participant can play in any league events

**Profiles**

- Participants can register as an individual player to participate in any league event
  - This is required to participate in the league as a player
  - This should only be done once per person (subject to league rules regarding multiple game accounts)
- Participants can register a team to participate in any league events specifically for teams
  - The participant registering the team become the team caption by default
  - This can be changed to another individual participant after team creation has finalized
  - Members of the team must also be registered individual participants to fill a roster slot on a team
- Participants should maintain the individual/team profile that they are responsible for. This means
  - Submitting roster change request in a timely manner for staff processing
  - Keeping name and aliases up-to-date so roster can be verified easily
  - Maintaining appropriate names/logos/colors

### Participant expectations

**Sportsmanship**

- Participants are expected to maintain good sportsmanship during active league sponsored events and in general
- Participants may report unsportsmanlike behavior as a league event with a detailed description of said behavior
- Participants may report and individual player or a participating team
  - A report to an individual affects only the single participants standing in the league
  - A report to a participating team affects the teams standing within the league (and all players on that roster)
- Unsportsmanlike behavior reports are reviewed by league staff to determine if consequences should be dealt
  - If approved by staff, the participant (individual or team) will receive a disciplinary strike
  - If not approved, no disciplinary strikes will be dealt, but a reason should be given for the rejection
- A participant that obtains a league staff determined number of disciplinary strikes will be disqualified from participating in league events
- Disciplinary strikes decay at a rate of -1 per 30 calendar days
  - Having 0 strikes means no decay will occur
  - Having 1 or more strikes will purge the last strike earned on the participants profile

**Unanticipated disruptions**

- Participants shall report in a timely manner when
  - Event times do not work with schedules
  - Event requirements (such as minimum participant count) cannot be met
- Participants shall report interruptions that prevent a fair contest from occurring
  - Game breaking bugs or other errors
  - Network disruptions occur during play
- Disruptions are reported as events that cause delay in a match event
  - Delays could mean a repeat play or forfeit
  - Staff (if available) should approve the resolution

### Events

**Creation**

- League staff are responsible for organizing the event within the software
  - Create the necessary resources for the event (brackets and divisions for matchmaking)
  - Select a start date from the event sign up period and a start date for the event start
- Software will provide an interface for selecting an event type (teams or individual participants)
- Software will provide an interface for staff to organize the event based on type
  - Showdown (Single elimination with 2 participants)
  - Single elimination bracket (requiring n-1 matches to be played for n participants)
  - Double elimination bracket (requiring 2n-2 matches to be played for n participants)
  - Round robin tournament (requiring {n choose 2} matches to be played for n participants)

**Progression**

- Matches are automatically declared when the event type is set
  - Match information is lazily filled out as the tournament progresses
  - Match start times may be set when participants or staff are certain of the start time
  - Match results are set after the match has played out and the bracket progresses
- Staff can update match or bracket information without approval
- Participants may submit request to progress the bracket in a certain manner, but it must be approved by staff

**Conclusion**

- Events are marked as concluded by staff along with a reason
- Typically, the reason will be declaring a winner or leaderboard
- Occasionally, the reason may be lack of participant interest
- Participants cannot request an event to conclude
  - They should forfeit or unregister if still allowed

## Usage scenarios

### League management tasks

**Creating a league**

> As a league administrator, I want to create a centralized hub for my league so that league information is easily available to both league staff and league participants

1) Authorize as league administrator
2) Create a new league by choosing a name and assigning assets to the league
3) Used the given league identifier to advertise the hub for the interested parties

**Assigning staff**

> As a league administrator, I want to assign additional individuals as staff members so that the workload of league administration is not put on the shoulders of 1 person

1) Have additional staff members authenticate as themselves within the application
2) Invite the new staff member to the league to fill the staff position
3) Additional staff member is added to the league and acquires the staff role within that league

**Responding to a ticket**

> As a league staff member, I want events that would modify the state of the league to be submitted as ticket so that approval needs to be given for the event to take place.

1) Event ticket is submitted by a staff member or a participant involving an issue/report/or other state change
2) Staff member picks up ticket and comes to a decision regarding the ticket
  - If approved, side effects of the ticket are applied to the league state
  - If denied, side effects are not applied to the league state
3) Application modifies league state according to side effects of the ticket

### Participant responsibilities

**Registering as an individual**

> As an interested individual participant, I want to register myself into a league so that I can participate in events sponsored by that league

1) Authenticate within the application to begin the registration process
2) Select the league that the registration process will register with
3) Submit the requested information on the individual registration form
4) Application will create a ticket for the individual registration to be finalized
5) Await a staff member to approve the ticket
6) New registrant gains the ability to sign up for events sponsored by the league they've registered for

**Modifying a player profile**

> As a registered individual participant, I want to be able to modify my league profile so that the profile on file reflects the most current information

1) Authenticate within the application to begin making changes
2) Submit the updated information on the profile edit form
3) Application creates a ticket for profile changes to be approved
4) Staff member approves or denies profile change request
5) Application applies profile changes if request is approved

**Registering as a team participant**

> As a registered individual participant, I want to be able to create a team will fellow individual participants so that we can participate in team-based events sponsored by that league

1) Authenticate within the application to begin the team registration process
2) Select the league the team will register with
3) Submit the requested information on the team registration form
4) Application will create a ticket for the team registration to be finalized
5) Await a staff member to approve the formation of a team
6) New registered team gains the ability to sign up for team events

**Modifying a team profile**

> As a team captain of a registered team, I want to be able to modify the league profile of the team so that the profile on file reflects the most current information

1) Authenticate within the application to begin making changes
2) Submit the updated information on the profile edit form
3) Application creates a ticket for team profile changes to be approved
4) Staff member approves or denies the profile change request
5) Application applies the profile changes if request is approved

**Modifying a roster**

> As a team captain of a registered team, I want to be able to add or remove individual participants from my team roster so that I can build a competitive team for team-based events sponsored by the league

1) Authenticate within the application to begin making roster changes
2) Submit the roster change request on the roster edit form
3) Application creates a ticker for the team roster change to be approved
4) Staff member approves or denies the roster change request
5) Application applies the roster changes if the request is approved

### Participant expectations

**Reporting unsportsmanlike behavior**

> As a league participant that is the victim of unsportsmanlike behavior, I want a mechanism available to report the inappropriate conduct so that the offending individual is incentivized to demonstrate better sportsmanship

1) Authenticate within the application to begin the unsportsmanlike complaint form
2) Gather the evidence of unsportsmanlike behavior towards yourself
3) Present the case on unsportsmanlike behavior against a team or individual participant
4) Application creates a ticket to review the evidence of the offending behavior
5) If staff deems the unsportsmanlike unacceptable, disciplinary action is taken on the ticket

**Staying in good standing**

> As a league participant, I want a mechanism to validate whether myself or other league participant have maintained a good standing within the league before being allowed to participate is league sponsored events

1) Application checks disciplinary standing when signing to participate in a league sponsored event
2) Participation is denied to any participant not meeting the good standing criteria

**Appealing a disciplinary action**

> As a league participant accused of unsportsmanlike behavior and has had disciplinary action taken, I want to be able to appeal the decision so that the disciplinary action might possibly be reverted

1) Application delivers notice of disciplinary action taken on a league individual
2) Accused league individual decides to appeal and begin the appeal form
3) Accused individual present their case to revert the disciplinary action taken
4) Await staff member to review counter arguments and decision to revert or not

### Event management

#### Showdowns

**Creation**

> As a league administrator, I want to be able to create a showdown tournament between two individual participants or two team participants so that the two participants can showdown against one another

1) Authenticate within the application as a league administrator
2) Create the league event and specify the type as a showdown
3) Set the rule set for showdown matches
4) Invite showdown participants to sign up

**Progression**

> As a league staff member, I want to approve the progression of a showdown match to update the event state so that the current state is unambiguously available

1) Receive match concluded event from a participant and approve winner

OR

1) Emit and automatically approve match concluded event as self

**Conclusion**

> As a league staff member, I want to certify a winner of a showdown event so that the event concludes

1) Certify the winner of the showdown and conclude the event

#### Single elimination tournaments

**Creation**

> As a league administrator, I want to be able to create single elimination tournament so that the superior participant emerges from a starting group of participants

1) Authenticate within the application as a league administrator
2) Create the league event and specify the type as a single elimination
3) Set the rule set for knockout matches
4) Invite participants to sign up

**Progression**

> As a league staff member, I want to approve the progression of a knockout match to update the event state so that the current state is unambiguously available

1) Receive match concluded event from a participant and approve winner

OR

1) Emit and automatically approve match concluded event as self

**Conclusion**

> As a league staff member, I want to certify a winner of a single elimination event so that the event concludes

1) Certify the winner of the single elimination tournament and conclude the event

#### Double elimination tournaments

**Creation**

> As a league administrator, I want to be able to create double elimination tournament so that the most resilient participant emerges from a starting group of participants

1) Authenticate within the application as a league administrator
2) Create the league event and specify the type as a double elimination
3) Set the rule set for demotion and knockout matches
4) Invite participants to sign up

**Progression**

> As a league staff member, I want to approve the progression of a demotion or  knockout match to update the event state so that the current state is unambiguously available

For demotion matches

1) Approve the match result from participant or self approved from staff member
2) Move losing team to loser's bracket
3) Keep winning team in current bracket

For knockout matches

1) Approve the match result from participant or self approved from staff member
2) Keep winning team in loser's bracket

**Conclusion**

> As a league staff member, I want to certify a winner of a double elimination event so that the event concludes

1) Certify the winner of the double elimination tournament and conclude the event

#### Round-robin tournaments

**Creation**

> As a league administrator, I want to sponsor round-robin tournament so that the most determined teams emerge from the starting group

1) Authenticate within the application as a league administrator
2) Create the league event and specify the type as a round-robin
3) Set the rule set for demotion and knockout matches
4) Invite participants to sign up

**Progression**

> As a league staff member, I want to approve the result of a play-all match to update the state of the event so that the current state is unambiguously available

1) Approve the match result from participant or self approved from staff member
2) Allow the next play-all matches to commence if both participating teams have played all previous matches

**Conclusion**

> As a league staff member, I want to certify a podium of leaders of a round-robin event so that the event concludes

1) Certify the top n teams of the round-robin tournament and conclude the event
