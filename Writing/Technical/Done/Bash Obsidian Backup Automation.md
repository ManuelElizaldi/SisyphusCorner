Since my background is in economics and never received formal training on computer science, there's still so much more about this field I need to learn. 

While searching for material to study I stumbled upon this series of lectures by MIT. They cover tools and topics usually not covered by a regular corriculum of CS. https://missing.csail.mit.edu/2026/

My first job involving the tools of programming to solve problems was more related to data analysis, no real development of software. It was more a way of using code, complimented by statistical analysis to explain what was going on with business problems. This was my first dipping my toes mome into the world of programming. I mostly used sql and python, now as a business intelligence developer my tool kit is increasing and I feel the demand for other tools. One of them is shell. 

This is a tool that I keep coming back to in projects in my current gig so I thought it necessary to learn more. 

I have a raspberry pi acting as a home server, it has a mounted ssd that is shared through my network using samba. This acts as the source directory for my obsidian vault. Everything from my notes, journal entries and other important text files live here. Having it hosted through smb allows me to use a synced obsidian vault from anywhere. But today, providence decided to teach me a lesson. 

My raspberry pi lost internet connection, my obsidian glitched and lost all of my notes from lesson 1. But I thought about the small things I learned from this lesson and decided to automate a auto sync process. 

My obsidian notes are also hosted on a private github repo. This acts as a backup to my knowledge base. 

As I was watching the introduction lesson on shell, my raspberry pi lost connection to the internet, my obsidian glitched and lost my notes on lesson 1. 

Frustrated I thought about applying what I just learned plus what I already knew about bash scripts and came up with a solution. Why not just schedule a cron job to see if there's any changes to the directory where I host my obsidian vault, if there are add it to my git hub repo. 

yes, of course, this will probably make the commit history it a bit messy but right now I am using version control as a way to store my obsidian vault. 

Problems and frustrations give way to solutions. 