.. _whining:

Whining
#######

Whining is a feature in Bugzilla that can regularly annoy users at
specified times.  Using this feature, users can execute saved searches
at specific times (e.g. the 15th of the month at midnight) or at
regular intervals (e.g. every 15 minutes on Sundays).  The results of the
searches are sent to the user, either as a single email or as one email
per bug, along with some descriptive text.

.. warning:: Throughout this section it will be assumed that all users are members
   of the bz_canusewhines group, membership in which is required in order
   to use the Whining system.  You can easily make all users members of
   the bz_canusewhines group by setting the User RegExp to ".*" (without
   the quotes).

   Also worth noting is the bz_canusewhineatothers group.  Members of this
   group can create whines for any user or group in Bugzilla using an
   extended form of the whining interface.  Features only available to
   members of the bz_canusewhineatothers group will be noted in the
   appropriate places.

.. note:: For whining to work, a special Perl script must be executed at regular
   intervals.  More information on this is available in :ref:`installation-whining`.

.. note:: This section does not cover the whineatnews.pl script.
   See :ref:`installation-whining-cron` for more information on
   The Whining Cron.

.. _whining-overview:

The Event
=========

The whining system defines an "Event" as one or more queries being
executed at regular intervals, with the results of said queries (if
there are any) being emailed to the user.  Events are created by
clicking on the "Add new event" button.

Once a new event is created, the first thing to set is the "Email
subject line".  The contents of this field will be used in the subject
line of every email generated by this event.  In addition to setting a
subject, space is provided to enter some descriptive text that will be
included at the top of each message (to help you in understanding why
you received the email in the first place).

The next step is to specify when the Event is to be run (the Schedule)
and what searches are to be performed (the Searches).

.. _whining-schedule:

Whining Schedule
================

Each whining event is associated with zero or more schedules.  A
schedule is used to specify when the search (specified below) is to be
run.  A new event starts out with no schedules (which means it will
never run, as it is not scheduled to run).  To add a schedule, press
the "Add a new schedule" button.

Each schedule includes an interval, which you use to tell Bugzilla
when the event should be run.  An event can be run on certain days of
the week, certain days of the month, during weekdays (defined as
Monday through Friday), or every day.

.. warning:: Be careful if you set your event to run on the 29th, 30th, or 31st of
   the month, as your event may not run exactly when expected.  If you
   want your event to run on the last day of the month, select "Last day
   of the month" as the interval.

Once you have specified the day(s) on which the event is to be run, you
should now specify the time at which the event is to be run.  You can
have the event run at a certain hour on the specified day(s), or
every hour, half-hour, or quarter-hour on the specified day(s).

If a single schedule does not execute an event as many times as you
would want, you can create another schedule for the same event.  For
example, if you want to run an event on days whose numbers are
divisible by seven, you would need to add four schedules to the event,
setting the schedules to run on the 7th, 14th, 21st, and 28th (one day
per schedule) at whatever time (or times) you choose.

.. note:: If you are a member of the bz_canusewhineatothers group, then you
   will be presented with another option: "Mail to".  Using this you
   can control who will receive the emails generated by this event.  You
   can choose to send the emails to a single user (identified by email
   address) or a single group (identified by group name).  To send to
   multiple users or groups, create a new schedule for each additional
   user/group.

.. _whining-query:

Whining Searches
================

Each whining event is associated with zero or more searches.  A search
is any saved search to be run as part of the specified schedule (see
above).  You start out without any searches associated with the event
(which means that the event will not run, as there will never be any
results to return).  To add a search, press the "Add a search" button.

The first field to examine in your newly added search is the Sort field.
Searches are run, and results included, in the order specified by the
Sort field.  Searches with smaller Sort values will run before searches
with bigger Sort values.

The next field to examine is the Search field.  This is where you
choose the actual search that is to be run.  Instead of defining search
parameters here, you are asked to choose from the list of saved
searches (the same list that appears at the bottom of every Bugzilla
page).  You are only allowed to choose from searches that you have
saved yourself (the default saved search, "My Bugs", is not a valid
choice).  If you do not have any saved searches, you can take this
opportunity to create one (see :ref:`list`).

.. note:: When running searches, the whining system acts as if you are the user
   executing the search.  This means that the whining system will ignore
   bugs that match your search but that you cannot access.

Once you have chosen the saved search to be executed, give the search a
descriptive title.  This title will appear in the email, above the
results of the search.  If you choose "One message per bug", the search
title will appear at the top of each email that contains a bug matching
your search.

Finally, decide if the results of the search should be sent in a single
email, or if each bug should appear in its own email.

.. warning:: Think carefully before checking the "One message per bug" box.  If
   you create a search that matches thousands of bugs, you will receive
   thousands of emails!

Saving Your Changes
===================

Once you have defined at least one schedule and created at least one
search, go ahead and "Update/Commit".  This will save your Event and make
it available for immediate execution.

.. note:: If you ever feel like deleting your event, you may do so using the
   "Remove Event" button in the upper-right corner of each Event.  You
   can also modify an existing event, so long as you "Update/Commit"
   after completing your modifications.
