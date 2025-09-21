+++
tags = ['Developer Log', 'Python', 'Linux', 'Networking', 'Home Lab', 'Virtual Environment', 'TrueNAS']
title = 'Developer Week 039'
date = 2025-04-14T07:50:07+01:00
draft = false
+++

![Developer Week 039](https://pbrazeale.github.io/images/devweek039.jpg)

## Projects

### Home Lab

- Installed TrueNAS SCALE on the Proxmox server
  - [Documented How](https://pbrazeale.github.io/posts/truenas-on-proxmox/)
  - Created Datasets
    - Including Backup folders for networks users
      - Implemented SMB shares
      - Edited ACLs to ensure only designated users have access to their folder.
      - Placed users in custom group
        - Established group permissions for a group folder
  - Setup Jellyfin app on TrueNAS
    - Created ACL group and user for Jellyfin admin and linked to designated folders
- Dealt with network issues on the main router.
  - Long-term solution is to install a new router and create a sub-network, to isolate devices based on levels of trust.
    - Likely hardwire all devices that aren't phones, and turn wifi into a purely untrusted network.

### AuthorLedger v2.0.0 ~80%

- Amazon Features 100% done, and all bugs resolved.
- Still researching to expand other functions.
- Ad Tracking features still in development but should finalize this week.

### DocX to Epub Format ~40%

- Software is rebuilt using Electron to encapsulate, JavaScript for the front end, and Python for the backend.
  - Python Requirements

```python
EbookLib==0.18
lxml==5.3.2
python-docx==1.1.2
six==1.17.0
typing_extensions==4.13.1
```

- Core problem solved: .epub files are now ~15% smaller than their .docx counterparts.

#### TODO

1. Research image compression options for embedding cover at the front of the .epub.
2. Create font options for embedding into .epub for Title, Chapter Title, and scene breaks.
3. Improve UI
   1. Implement preview options before export
   2. Design visuals based on modern UI principles of minimalism
4. Test further to ensure broad file layout support.
5. Launch beta

## Courses

### Boot.Dev Learn Python (9.1/14.8) **~48%**

- Good refresher thus far, but there are aspects of Python I'm not using on a regular basis and need to learn.

### LeetCode/NeetCode (150)

- Solved 6 Arrays & Hashing
  - Solving 1 per day, along with repeating all before
    - Until I can explain and solve the problem in under 10 minutes
    - Practicing my ability to talk and code at the same time (_not as easy as it looks LOL_)

## Application Process

### Applications (72/1,000) **~7.2%**

- 35 Rejections
- 1 proceed to next round
- 37 waiting/no response

1 proceed to next round out of 68 is way above my expectations! This is a positive sign that my resume is tighter than expected after last weeks revamp; especially since the advancement came from a revamped resume application.

_Though of course it could all be coincidence. I'm not about to A/B test my resumes in a live environment, aside from highlighting skills based on the role I'm applying for._
