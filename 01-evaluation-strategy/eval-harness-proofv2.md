# First LLM-as-a-Judge Eval, Module 1

## Version A, Concise, system prompt used

You are an executive briefing assistant.
Summarize in exactly 3 bullet points under 60 words. No preamble, no extra text.

## Version B, Narrative, system prompt used

You are a PR communications assistant.
Write a 100-word narrative summary highlighting wins first, then risks and next steps. Keep a positive tone. No bullets.

## Eval setup, dataset name + judge model/family

Dataset: Module1Output, Evaluator: Conciseness (LLM-as-a-Judge), Generator: Sonnet 5.5 from Claude,

## Cold-start, the prompt you used to seed a starter dataset

Generate 20 example rows for evaluating email-summary quality. Each row: input email + candidate summary + a first-pass label (good/bad) + one-line reason. Make ~half concise/faithful (good) and half verbose or inaccurate (bad). Return as a markdown table.

## Your definition of good vs bad (golden-set criteria), the graded part, write your own

#	Input email	Candidate summary	Label	Reason
1	Hi team, the Q3 planning meeting moved from Tuesday 2pm to Thursday 10am. Same room (B204). Please update your calendars.	Q3 planning meeting moved to Thursday 10am, same room (B204).	good	Captures the new time and the unchanged room.
2	Hi team, the Q3 planning meeting moved from Tuesday 2pm to Thursday 10am. Same room (B204). Please update your calendars.	The Q3 planning meeting has been rescheduled to Friday at 10am in a new room, so everyone should reschedule their other commitments accordingly.	bad	Wrong day, wrong room, and invents a request.
3	Your invoice #4471 for $1,250 is due Oct 31. Pay online or by bank transfer. Late payments incur a 2% fee.	Invoice #4471 ($1,250) is due Oct 31; a 2% fee applies if paid late.	good	Accurate amount, date, and penalty.
4	Your invoice #4471 for $1,250 is due Oct 31. Pay online or by bank transfer. Late payments incur a 2% fee.	This email is an invoice from a vendor. It talks about a payment and mentions some details about how to pay and when, and there is also something about fees if you are late, so you should read it carefully.	bad	Verbose and vague; omits the amount, date, and fee.
5	Hey Dávid, can you review the attached PRD by EOD Wednesday? Legal needs sign-off before Friday’s launch review. Thanks, Priya	Priya asks Dávid to review the attached PRD by end of day Wednesday so Legal can sign off before Friday’s launch review.	good	Keeps the requester, deadline, and reason.
6	Hey Dávid, can you review the attached PRD by EOD Wednesday? Legal needs sign-off before Friday’s launch review. Thanks, Priya	Priya has completed the PRD and Legal has approved it for Friday’s launch.	bad	Reverses the meaning: the review is requested and approval is pending.
7	We’re sorry your order #8820 arrived damaged. We’ve issued a full refund of $89.99, which will appear in 3-5 business days. No need to return the item.	Order #8820 arrived damaged; full refund of $89.99 issued, arriving in 3-5 business days, no return needed.	good	Complete and faithful.
8	We’re sorry your order #8820 arrived damaged. We’ve issued a full refund of $89.99, which will appear in 3-5 business days. No need to return the item.	The company apologized for the damaged order and offered a 50% discount on your next purchase. Please ship the item back within 14 days.	bad	Fabricates a discount and a return requirement; contradicts the source.
9	Reminder: the office will be closed Monday Oct 14 for the holiday. Normal hours resume Tuesday.	Office closed Monday Oct 14 for the holiday; reopens Tuesday.	good	Short and accurate.
10	Reminder: the office will be closed Monday Oct 14 for the holiday. Normal hours resume Tuesday.	In this email, the sender reminds all of the recipients that, because of an upcoming holiday that will take place soon, the office building will unfortunately be closed for one day, and that after this closure everything will go back to how it normally is, with regular hours.	bad	Wordy, no new information, and drops the specific date.
11	Hi, I’m interested in the Enterprise plan for 200 seats. Can you send pricing and a demo slot next week? - Marco, Acme Corp	Marco (Acme Corp) wants Enterprise plan pricing for 200 seats and a demo next week.	good	Includes the who, what, quantity, and ask.
12	Hi, I’m interested in the Enterprise plan for 200 seats. Can you send pricing and a demo slot next week? - Marco, Acme Corp	Marco from Acme wants to cancel his Enterprise subscription and asks for a refund.	bad	Wrong intent entirely; hallucinated cancellation.
13	Server db-02 hit 95% disk at 03:12 UTC. Cleared old logs, now at 61%. No customer impact. Follow-up: add disk alert at 80%.	db-02 reached 95% disk at 03:12 UTC; logs cleared, now 61%, no customer impact. Follow-up: add an 80% disk alert.	good	Covers the incident, resolution, impact, and action item.
14	Server db-02 hit 95% disk at 03:12 UTC. Cleared old logs, now at 61%. No customer impact. Follow-up: add disk alert at 80%.	Major outage on db-02 caused customer downtime overnight; the disk is still nearly full and the team is investigating.	bad	Contradicts the source on impact and current state.
15	Congrats! You’ve been selected for the Senior PM role. Offer letter attached. Please sign and return by Oct 20. Start date: Nov 3.	Selected for Senior PM; sign and return the attached offer letter by Oct 20. Start date Nov 3.	good	Preserves the key dates and action.
16	Congrats! You’ve been selected for the Senior PM role. Offer letter attached. Please sign and return by Oct 20. Start date: Nov 3.	You got the job as a Principal PM with a starting salary of $180k, starting Nov 1. Respond when convenient.	bad	Invents the title, salary, and wrong start date; drops the deadline.
17	Team, sprint demo is Friday 3pm. Please have your slides in the shared folder by Thursday noon. Keep demos to 5 minutes.	Sprint demo Friday 3pm; slides due in the shared folder by Thursday noon; 5 minutes each.	good	Faithful and complete.
18	Team, sprint demo is Friday 3pm. Please have your slides in the shared folder by Thursday noon. Keep demos to 5 minutes.	There is a demo on Friday. Slides are needed. The demos should be kept short. Also, it is probably a good idea to practice beforehand and bring snacks.	bad	Vague on times and limits; adds unsupported suggestions.
19	Your password was changed on Oct 11 at 14:05 from a new device in Austin, TX. If this wasn’t you, reset it immediately and contact security@corp.com.	Password changed Oct 11, 14:05, from a new device in Austin, TX. If not you, reset it and contact security@corp.com.	good	Retains the security-critical details and the action.
20	Your password was changed on Oct 11 at 14:05 from a new device in Austin, TX. If this wasn’t you, reset it immediately and contact security@corp.com.	Your account was hacked from London and your data has been stolen; call the police right away.	bad	Alarmist; wrong location and fabricated breach.

## Screenshots, links or repo paths (optional if you followed the demo)

_…_

