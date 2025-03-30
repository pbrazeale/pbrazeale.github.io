+++
tags = ['Developer Log', 'CompTIA', 'Azure', 'Python', 'Linux', 'Security+', 'shell']
title = 'Developer Week 037'
date = 2025-03-30T14:36:07+01:00
draft = false
+++

## Certification Progress
### Microsoft Certified: Azure Fundamentals (33%)

[AZ-900 Azure Fundamentals](https://learn.microsoft.com/en-us/credentials/certifications/azure-fundamentals/?practice-assessment-type=certification)

## Projects

### 100 Days of Code: The Complete Python Pro Bootcamp (42/100)
#### Day 041 HTML
[Stack Overflow Post](https://stackoverflow.com/questions/40155875/how-can-i-do-tag-wrapping-in-visual-studio-code)
>Embedded [Emmet](https://code.visualstudio.com/docs/editor/emmet) could do the trick:
>1. Select text (optional)
>2. Open command palette (usually Ctrl+Shift+P)
>3. Execute `Emmet: Wrap with Abbreviation`
>4. Enter a tag `div` (or an abbreviation `.wrapper>p`)
>5. Hit Enter
Command can be assigned to a keybinding.
[![enter image description here](https://i.sstatic.net/UQgrQ.gif)](https://i.sstatic.net/UQgrQ.gif)

- This will save me some copy paste tediousness. 



### pbrazeale.github.io
- [Updated Hugo Blog](https://pbrazeale.github.io)

Took the plunge and switched to *Hugo* from *Jekyll* after I ran into an issue uploading a markdown table into my post. Being able to just copy paste from my obsidian  


### AuthorLedger ~45%
Updating the python project I made for CS50P.

Working Logo/Icon:
![[AuthorLedger logo.webp]]

Ultimate objective is to create a complete application for managing and tracking indie author performance for authors and/or small publishers. 
#### Design: 
1. Create a localized SQL database for royalty reports from Amazon
2. Utilize PyQt6 for the GUI
3. pandas for the data processing
4. openpyxl for importing the .xlsx files
5. matplotlib for the charts
6. fpdf2 for exporting .pdf
#### Expansion:
1. Update the database to automatically convert to USD
2. Allow for fine tuning selection based upon:
	1. Book Title
		1. Create Series Titles that auto select associated books
	2. Authors
	3. Platform
	4. Title Format
		1. ebook
		2. KU
		3. paperback
		4. hardback
		5. audiobook
3. Display charts that show revenue comparison based on:
	1. Platform
	2. Physical vs Digital
	3. Digital breakdown
		1. KU
		2. ebook
		3. audiobook
	4. Physical breakdown
		1. paperback
		2. hardback
4. Add in additional databased to support all major sales platform
	1. Amazon *done*
	2. Nook
	3. iBooks
	4. Google Play
	5. Draft 2 Digital *most complex as it requires all the platforms they publish to*
5. Additional Functionality Expansion
	1. Create a Revenue and Expanse tracker
		1. Display and Export simple P&Ls
	2. Ad ROI tracker
		1. Convert my current excel formula template into an additional tab within the application
		2. Track ad performance based upon
			1. Platform
			2. Cost
			3. Clicks
			4. Conversion
		3. Use tracking to create reports:
			1. Ad level ROI
				1. Single title
				2. Series level
			2. Platform ROI
				1. Single title
				2. Series level

## Courses

### Microsoft Azure Fundamentals AZ-900 (5.11/11.6) **~44%**

[Course AZ-900T00-A: Microsoft Azure Fundamentals](https://learn.microsoft.com/en-us/training/courses/az-900t00)


## Books

[**The Linux Command Line**](https://archive.org/details/tlcl-19.01) (411/594) **~69%**

## 9 Months Obsidian Takeaway
I wrote a full [article](https://pbrazeale.github.io/posts/9-months-obsidian-takeaways/) detailing my entire process and thoughts on the advantages of Obsidian in my life.

Literally the same day, Mischa referenced [JohnnyDecimal](https://johnnydecimal.com/) which I'd not heard of, but is clearly a more refined version of what I'm already doing with my 100 folder system. Now I'm in an awkward position where I feel I'm under utilizing my Obsidian vault, and I instantly loved the idea of mapping that file structure onto my actual file storage on my computers. 

With the new Proxmox server, this would be an ideal time to implement a proper organization schema.
