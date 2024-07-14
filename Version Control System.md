# A better version control system

## The problem with Git

Well, Git has a horrible UX like all command line tools but the biggest problem with it is that it stores names in the commit history. We are assigned legal names against our consent by the system and storing names permanently disproportionally hurts women and trans people.

### Scenario #1: Abusive marriage

A woman marries a man who turns out to be exceptionally abusive. She already changed her last name to her husband's name but the abuse forces her to file for divorce and change her last name again. But the company she has been working in demands using legal names so every time she looks at her old commits, she sees her ex-husband's last name.

This leads to hurt feelings, lost productivity, lost profits for the company and potentially leaving the company altogether just to not be reminded of her abusive husband.

### Scenario #2: Gender transition

Well, things are way more clear cut in this case. Trans people call their old names assigned to them against their consent ["deadnames"](https://en.wikipedia.org/wiki/Deadnaming) for a reason.

So, again, seeing deadname leads to hurt feelings, lost productivity, lost profits for the company and potentially leaving the company altogether just to not be reminded of your deadname.

## Solution

Store numerical identifiers instead of names and have a separate database storing committers' information that is mutable. Then the UI would query the database and show the latest information when viewing commits.
