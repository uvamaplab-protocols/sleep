# Follow-up questions

Open items after building the protocol from the researcher's four Word documents and testing
releases 0.0.4 and 0.0.5 on a phone with the `sleep-t` code (2026-10-30).

## For the researcher

1. **Which symptom list?** The sleep study summary gives every group a daily list of 11 symptoms:
   stomach pains, headache, migraine, backache, fatigue, nausea, mood swings, difficulty
   concentrating, anxiety, irritability, sadness. "Additional Questions to add to both apps" gives the
   two female groups a different list of 12: abdominal cramps, bloating, back pain, headaches,
   migraines, nausea, mood swings, irritability, anxiety, sadness, feeling overwhelmed, feeling
   angry. The app uses the 11 for everyone. Should the female groups get the 12 instead, or both?
2. **30 or 45 days?** The newer summary says the Oura Ring tracks sleep for 45 days and ovulation
   tests are logged over 45 days, but its surveys and daily questions run for 30. The app runs the
   daily check-in for 30 days, opens the final surveys with the 30th check-in, and lets test days be
   set up to 45 days ahead.
3. **Who gets the contraception question?** The newer summary says only participants on the pill
   get it; the other says everyone in the group, whatever the method. The app asks everyone in the
   hormonal contraception group. The "Additional Questions" doc also words it differently ("Did
   you take your birth control today as prescribed?"); the app uses "Did you take/use your
   hormonal contraception today, per your regular schedule?".
4. **Contraception methods.** One summary lists pill, shot, IUD, patch or ring; the other pill, shot
   or ring. The group picker shows the longer list.
5. **Daily question for males.** The newer summary gives males the daily symptom question; the older
   one gives them none. The app asks it.
6. **Baseline at enrollment.** The four baseline surveys run right after enrolling, about 60
   screens, and must be finished before the app opens (participants can stop and resume). Is that
   the intended "Day 1"?
7. **When the check-ins and final surveys open.** The daily check-in opens at 8 PM and stays open
   until 8 PM the next day. The first opens the second evening after enrollment: someone enrolling
   on Oct 30 just after midnight first sees it on Oct 31 at 8 PM. The final surveys open with the
   30th check-in and stay open 3 days. Should the check-ins start the evening of enrollment
   (`skip: 0` in `src/surveys.json`)?
8. **PSQI changes.** Its license allows no modifications without permission from the University of
   Pittsburgh. The app shows one question per screen; the bedtime and wake-time pickers start at
   11:00 PM and 7:00 AM, so a participant can leave the default; and 5j and 10e ask how often first,
   then for a description only if the answer isn't "Not during the past month". Are these OK, or do
   they need permission?
9. **QDS question 1.** It reads "How many days per week out of the past 30 did you drink any
   alcohol?", as in the document. Confirm that's the intended wording.
10. **Photo of the ovulation test strip.** Survey pages in the app can't take photos. The newer
    "Additional Questions" doc asks only for positive or negative, which is what the app records. Is
    the photo still needed?
11. **"None of these" symptom option.** Added so participants with no symptoms can answer. OK?
12. **Who enters the ovulation test days?** The researcher picks up to 5 days per participant. The app
    reminds the participant on each day entered under My Test Days, so either the participant or
    staff at enrollment has to enter them.
13. **Oura Ring data.** Digital Trails can connect to a participant's Oura account. Should the app do
    that, or does the team collect Oura data separately?
14. **Team and contact information, and the app name.** The app has no team page, FAQ or contact
    email, and shows "Sleep Study" (the summary proposed "SleepStudy").

## For study setup

15. **Config flow on every code.** The app needs the code's config flow set to
    `flow://flows/configs.json`, which asks for the participant's group. Without it, enrolling fails
    with "Digital Trails couldn't start Sleep". It is set on `sleep-t` now; the production code
    needs it too.
16. **Changing a participant's group.** Settings has no Configuration row for `sleep-t`, so the only
    way to switch someone between groups is to unenroll and re-enroll. Turning on
    `show_settings_config` would let staff change it in place.
17. **Reminder timing (app, not protocol).** Android delivers the app's reminders inexactly, up to an
    hour after 8 PM, and every Digital Trails notification uses the same notification id, so a newer
    reminder replaces an older one.
18. **Portal check.** Test data was sent from `sleep-t` on Oct 30 between about 12:00 and 12:20 AM:
    naturally menstruating (twice), male and hormonal contraception enrollments, both batteries, the
    daily check-in and an ovulation result. Confirm it shows in the portal with the expected output
    names (`baseline_*`, `final_*`, `daily_*`, `opk_*`, `config_population`).
