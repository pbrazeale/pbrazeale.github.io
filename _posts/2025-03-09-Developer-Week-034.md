## Projects
### Security+ Acronym Flash Cards
This is the first project I'm proud enough of to pin on my github profile and writeup a proper README for:
[https://github.com/pbrazeale/security_plus_acronym_flash_cards](https://github.com/pbrazeale/security_plus_acronym_flash_cards)

Took Day 031 and expanded upon it to give myself *and others*, a study tool for the long this of Acronyms.

I had a PDF list, which wasn't fully formatted. 
1. First was to use GPT to clean the list all on one line.
2. Was to practice my python skills and pandas.
	1. Ran into an issue where pandas was separating on commas within the "Spelled Out" column, so I used GPT again to write up a quick line by line filter.
3. With the clean "acronym_list.csv" I could start the build.
4. With the new "acronym_list.csv" modifying the flashcard code app was as simple as modifying file names and uploading.

### 100 Days of Code: The Complete Python Pro Bootcamp (33/100)
#### Day 028 Pomodoro Timer
[https://github.com/pbrazeale/100-Days-of-Code/tree/main/day_028_pomodoro](https://github.com/pbrazeale/100-Days-of-Code/tree/main/day_028_pomodoro)
Built a pomodoro timer with Tkinter.

This was fun and far easier than I thought it would be at first glance. Was able to solve each section ahead of the instructional videos.
#### Day 029 & 030 Password Generator
[https://github.com/pbrazeale/100-Days-of-Code/tree/main/day_029_password_manager](https://github.com/pbrazeale/100-Days-of-Code/tree/main/day_029_password_manager)
Built a password generator with Tkinter, random, and pyperclip.
!["images\password_generator.gif"]
##### Git Restore Deleted File
Accidentally deleted `day_029_password_manager/main.py` thankfully stack overflow saved me: [https://stackoverflow.com/questions/953481/how-do-i-find-and-restore-a-deleted-file-in-a-git-repository](https://stackoverflow.com/questions/953481/how-do-i-find-and-restore-a-deleted-file-in-a-git-repository)

`git log --diff-filter=D --summary` log, difference filtered by D (delete), summary for short.

`git checkout e4e6d4d5e5c59c69f3bd7be2~1 path/to/file.ext` ~1 step back one hash from where the file was deleted and pull the file path. 

#### Day 033 ISS Overhead Notifier
[https://github.com/pbrazeale/100-Days-of-Code/tree/main/day_033_iss_overhead_notifier](https://github.com/pbrazeale/100-Days-of-Code/tree/main/day_033_iss_overhead_notifier)
Built an app that uses two APIs to track sunset and ISS location, and then sends an email notification via smtplib.

Built functions:
- iss_call()
- sun_call()
- is_dark()
- iss_overhead()
- send_email()
- check_10_min()
- main()

This was an excellent project, and I already see how using APIs and cronjobs to build an automated pipeline would save me hours of work, and more importantly create automatic notifications so that I can stop checking dashboards manually throughout the day. Already thinking through project ideas...


## Courses
### CompTIA Security+ SY0-701 (1.4/5.6) **~12%**
[Professor Messer's lecture series:](https://www.youtube.com/watch?v=KiEptGbnEBc&list=PLG49S3nxzAnl4QDVqK-hOnoqcSKEIDDuv)

[CompTIA's Exam Objectives:](https://www.comptia.org/training/resources/exam-objectives)

[Security+ Acronym Flash Cards:](https://github.com/pbrazeale/security_plus_acronym_flash_cards)

### Boot.Dev Learn Git (11.6/11.6) **Completed**
Happened to get this in my feed: [https://www.youtube.com/watch?v=rH3zE7VlIMs](https://www.youtube.com/watch?v=rH3zE7VlIMs)

[boot.dev](https://boot.dev) offers the course material for free also, though I recommend following along with the above YouTube video and starting a new director to play with.

### Boot.Dev Learn Linux (2.15/6.6) **~36%**


## Books
**The Linux Command Line** (144/594)

**How Linux Works by Brian Ward** (204/366)

**LPIC-1 Exam 101** (11/554)
