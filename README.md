
---

# Compound Integration to Detect Shift Gaps and Empty Shifts
This is a compound integration to solve that problem of whether any of my groups have gaps in the shifts or shifts with no members.  Whilst you can do this through the web interface it relies on you going in and looking.  With this new integration you can have a scheduled task kick this off every day to report on a list of groups you provide and it will message you with any gaps and empty shifts.

It's not got all the bells and whistles, it doesn't have nice message formatting etc, but should give you a great head start.  It only looks for shifts that aren't consecutive so will also fire if your shifts overlap.  It also needs tweaking to send you and all clear message if there are no issues.  They are all easy for you to fix, I wanted you to have some of the fun!

Regarding scaling, this isn't going to work for big numbers of groups as the IB script will timeout.  How big you can go, who knows.  Give it a try and see.

# How it works

You send the Shift Gaps message with a comma separated list of groups to check.  This actually goes to a dummy email recipient, you don't need to receive this message.  

The IB script then goes through each of the groups, looking up the On Call data for the following day and 7 days thereafter.  It analyses the data for shifts that aren't consecutive and ones that have no members.  It works out who sent the original Shift Gaps message and sends them the collated results via the Shift Gaps Results form.


# Pre-Requisites

* An xMatters account.
* Developer access.


# Files

* [ShiftGaps.zip](ShiftGaps.zip) - The comm plan (that has all the scripts and such).
* [Shift_Gaps_Script.txt](Shift_Gaps_Script.txt) - The Integration Builder JS to setup the outbound integration into xMatters , should you need it standalone to the Comm Plan.  It uses moment.js as a shared library (www.momentjs.com).
* [Shift_Gaps_and_Empty_Shifts.mov](Media/Shift_Gaps_and_Empty_Shifts.mov) - Video example of the finished integration.


# Installation


## The set up (xMatters)

1. Install the Shift Gaps communication plan attached.
2. Edit the Shift Gaps form, set to send email only and change the recipient to some user with a real but junk email address, you don't need to see this message.  Set expiry to 3 minutes.  Set to Web UI and mobile.  I'd hide the recipients, handling etc so the form just shows the box for the group list.
3. Edit the Shift Gaps Results form, remove voice call and SMS (I haven't set formats for them, you could add them yourself).  You don't need a recipient on this one, IB will send it to the original sender of Shift Gaps. Set to Web Service only.
4. Copy the Shift Gaps Result Web Service URL, edit the outbound IB script and set the path on the message send at the bottom to this new URL.
5. Set permissions on the scripts etc.

# Testing

Send a Shifts Gap message with a comma separated list of groups.  Within a minute you'll be messaged back with details of any gaps or empty shifts!


# Troubleshooting

Check the activity stream on the outbound integrations.
If you're still stuck, reach out to an xPert. 