---
description: Show live check-in numbers for an Eventrise event, or check someone in
argument-hint: "[event name] [attendee name or email to check in]"
---

Use the `attendees-and-checkin` skill and the rules in `eventrise-basics`.

Request: $ARGUMENTS

Find the event (ask if it's unclear). If the request names a person, find their tickets, confirm the match, and check them in. Otherwise report how many people have checked in against tickets issued, by ticket type.
