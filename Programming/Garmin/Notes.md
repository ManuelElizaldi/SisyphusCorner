Look up word _reversibility_, _backoff_

GarminConnect package, phase 1, get data back, test the logic 

We can get very specific with this data, but why load my database when I can easily get it from the garmin servers. For now I want to only focus on summaries, overall analysis. Weekly and monthly 

----
# Roadmap
Before next session, one thing to do without me: write in your `roadmap.md` a plain-English list of which endpoints your nightly pull will hit and what each one gives you. Not code. Just the menu. That list _is_ the spec for Phase 1's ingestion module, and writing it forces you to open the reference notebook and run the candidates against your own account.

# Sleep 
Pull general and specific for dashboard on ESP board
- `api.get_sleep_daily('2026-09-01','2026-09-03')`
	- This one is for ranges and gives a general overview
- `api.get_sleep_data('2026-09-03')` this is specific 
	- pull this daily? 

# General health stats
api.


### Memory concern
How much data should I be holding on the database? 
- for the AI model 
	- 2 to 3 months of data is enough? 
- screen description? Should only be displaying weekly info? unless I set up a 2nd page for monthly stats
