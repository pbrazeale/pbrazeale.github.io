+++
tags = ['Developer Log', 'AI', 'NovelFoundry']
title = 'Developer Week 075'
date = 2025-12-21T10:14:27+01:00
draft = false
+++

## NovelFoundry

### Frontend

- Shipped latest article [How to Perform a Beat Audit on Your Chapter](https://novelfoundry.com/articles/chapter-beat-audit) along with the accompanying dawrven council scene to act as a example here and moving forward.
- Updated website to use [vite-react-ssg](https://github.com/Daydreamer-riri/vite-react-ssg) to transition the SEO articles away from the SPA (single page application) design, and into a static site; much like HUGO does for this site. Updated site creation to force better SEO rich `<head>` sections during build time when converting .md articles.
- Created a CI/CD script that will automatically build, update, upload, and push the sitemap.xml for maximizing site indexing possibilities.
  - Thus far 100% success rate.
  - Only idea I have for expansion is to create a full fledged /sitemap page which can be automatically built at the same time to help with user navigation and improve indexing if/when the site grows to 1,000s of pages.

### Backend

- Created the APIs with Flask and tied into Supabase using their python module and [documentation](https://supabase.com/docs/reference/python/introduction). Authentication is up and working. Will implement Google auth before full access phase.
  - Backend is fully functional for handling file uploads and providing the user access to delete their manuscripts once uploaded.
    - Still need to refine the document controls within the bucket.
  - When it comes to the user's profile that happens directly from the application to Supabase.
- Celery is integrated to create workers with logging, to accomplish the editing pipeline; allowing for modification and splintering of the tasks depending on manuscript feedback triggers.
  - Logging is tried into my ability to report live performance tracking to the user.
  - Logging allows for errors to be captured and tracked in case the user doesn't get their reports, and will allow for manual rerunning of the tasks that fail, rather than the entire pipeline (saving token cost). Eventually the objective will be to build out an automated process to handle failed edits.
- Converted the original version of the local prompting engine, and refactored it to work in the new software. Modified it to allow for easier modifications moving forward. Eventually I'll need to build an admin dashboard to facilitate rapid testing and deployment.
- Created the ability for reports to be shown on the front end.
  - Updated the reports to link to a "download report" button that created a signed download URL.
  - Created a "Download All Reports" which creates a .zip folder within the bucket and then allows the user to download it.
    - Updated the backed to check for .zip to prevent multiple .zip folders from being created.
    - Identified a potential bug with my design, and fixed it. Centered around the way supabase storage buckets hold files, but now I've worked around this by updating my database; which is best practice for making auditing easier.
- Updated the backend to create a analysis locked per manuscript, so users can't run reports more than once per manuscript version.

#### Application Layer

- Redesigned the user dashboard to showcase folders (their project level view). Within those folders are the manuscripts (be it versions or series), and then within that manuscript can be found the editorial feedback.
  - Will constantly seek feedback from the beta team to identify if this design is intuitive. The core objective is that a user is able to log in for the first time, and instantly understand how to upload a manuscript, request edits, and then download their finalized reports.
- Modified the application to use live updates of the software progress as the workers complete tasks and update the database.
- Created a timer to show the user their ETA until the reports are done.
  - Locks out the dashboard while the reports are running. Will unlock once all are complete, or if one fails. Upon a failure there will be an alert so that user can report it to me.
    - Need to figure out a good way to automate reruns so that the user can get a complete analysis upon failure. Also need to figure out how to stop the user from using the "Download All" where there has been a failure, but still allow access to the individual reports.

### Database

- Created the storage buckets on Supabase and linked up the file uploads within the database via tables depending on which type of file it is.
- Updated the AI pipeline to automatically track the token usage and then report/log the costs. This will allow me to create an admin dashboard for seeing the power users, and run reports to show the editing phases that can best be optimized to reduce LLM costs.
