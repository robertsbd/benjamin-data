---
title: "My Business Stack"
date: 2025-01-18
---

As I set up my new business, Gamma Data, I find myself reflecting on its structure and the foundational choices I’ve made. 

With my first client onboard, the necessary HMRC documents sorted, an accountant hired, business insurance in place, my initial business proposition drafted, and financial processes beginning to take shape, I’ve reached a significant milestone.

Starting your own business gives you the unique opportunity to design not just your services but also the kind of business you want to run. In this post, I’ll share my thoughts on the tech stack that underpins my business—intentionally centered around Open Source and Linux wherever possible.

This choice stems from a combination of personal passion and practicality. I’ve long been a fan of Open Source and Linux, but more importantly, I’ve noticed just how many subscription-based services are marketed to new businesses: graphic design software, development tools, bookkeeping platforms, office suites, website hosting, email hosting—the list goes on. These services no doubt help get your businesses up and running quickly, but their cumulative costs can erode margins. And, I don't know much, but I do know that sales and margins are crucial to business viability.

To that end, here’s a breakdown of my business “tech stack,” which prioritizes cost-efficiency and independence by leveraging Open Source and Linux solutions wherever practical.

## The Stack

### Office Productivity
The only piece of software I a have a life-long commitment to is Emacs. And woth Org-mode it becomes super-powered Emacs. It serves as my all-in-one solution for note-taking, task management, project tracking, development, and more. Emacs truly minimizes my reliance on multiple subscription services.

For standard office productivity tasks, I use Microsoft Office. While LibreOffice is a solid Open Source alternative, Microsoft Office’s ubiquity ensures ease of interoperability with clients.

### Web & Email

#### Hosting
For web hosting, I’ve opted for [Carrd.co](https://carrd.co), which lets you create simple, one-page websites. At just £16 per year for a custom domain, it’s far more cost-effective than many other platforms. At this stage, I don’t need anything beyond a straightforward website.  
[Visit my website](https://www.gamma-data.co.uk)

#### Blog
My blog is hosted on [GitHub Pages](https://pages.github.com), a free and reliable web hosting solution. If my web needs ever become more sophisticated I may migrate my hosting across to Github Pages given that it is free - although most likely because Microsoft is using the content to train up their LLMs.

### Email
I use ProtonMail, a service I’ve trusted personally for years due to its strong focus on privacy and security. A custom domain subscription costs less than £5 a month.  
[Send me a message](https://www.gamma-data.co.uk#contact)

### Bookkeeping
For accounting, I rely on [GnuCash](https://gnucash.org), a free and Open Source solution. While its interface is dated, it’s more than sufficient for my needs. It handles everything from invoicing to managing Accounts Payable/Receivable, generating Profit and Loss statements, and monitoring cash flow. What more can I possibly need. Although many people swear by the big online tools, there cost doesn't seem justified having tried them out.

### Computer Operating Systems
My primary operating system is Linux, specifically the Fedora distribution. I previously used Arch Linux but, for a daily driver, I need to not be living in configuration files to keep the system running. I will however still be running Arch on my non-core systems, as it is fun!

That said, I also dual-boot into Windows, and the two reasons for this is: 1) the Microsoft Office suite is unavoidable when working with clients, and while the web version is available on Linux, it’s often easier to use the native applications in Windows; and 2) the cloud backup solution I am using doesn't run on Linux.

### Backup and Cloud Storage
For backups and storage, I’ve set up a network-attached storage (NAS) system using a Raspberry Pi. Syncthing ensures my data is synchronized between the NAS and my laptop, both Linux and Windows. I use Apple’s iCloud for offsite backup, providing redundancy in case of local hardware failure. Weekly and monthly backups further safeguard my data.

While I’m not entirely comfortable using Apple for cloud storage, the reality is that if it isn't Apple by data is going to be on Azure, Amazon, or Google. Indeed, I believe that iCloud storage utilizes Amazon and Google data centers.

---

By leveraging Open Source tools and carefully selecting cost-effective services, I’ve built a tech stack that aligns with my values and keeps costs manageable. If you’re considering starting your own business, I hope this overview offers some inspiration for crafting a stack that works for you.

[Contact me](https://www.gamma-data.co.uk#contact)
