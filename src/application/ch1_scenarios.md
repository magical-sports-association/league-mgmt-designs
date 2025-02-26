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
