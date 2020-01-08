# NFL_moneyline
currently only successful betting strategy, as of Jan2020

Overall strategy
I) Pull  game data
  a) use scrapR to pull all individual stats for each game 
  b) compute the stats delta between the two teams for each game (all stats deltas are relative to home team)
  c) include outcome
  d) calculate point differential and win totals between each team for each game
  e) calculate a strength of schedule by looking at the win totals of each teams opponents
  f) calculate the rolling 5 game average for each of these features
  g) save flat file.
II) Prep Spread Data
  a) Import Betting data (spread, moneyline and o/u), shared from wheel, from 10-18
  b) Regex team names
  c) merge w/ game data 
III) Create model 
  a) merge the above two together using unique ID of "HomeTeam" concatenated with "Game Date"
  b) Build a "full model" using all available NFLscrapR stats + OpeningSpread + Spread Movement + Opening OverUnder + Week
  nb: i tried to iteratively remove features, but the model just became too overfit.  The full model works best out of sample
 IV) Score the model 
  a) model was able to predict winner straight up ~62.5% of the time
  b) Convert moneyline into a percentage needed to break-even
  c) Calculate my probability to win for the home and away team
  d) compare each of those probabilityes to the moneyline percentage conversion.  These two numbers divided by each other equals the expected value
  e) I tested many different strategies
      i) bet each game
      ii) bet games w/ only expected values greater than a threshold (i.e, 10,20,30)
      iii) bet constant amount each game or "LetItRide" strategy
  V) Summary
  i) constant amount each game:
      if you bet a constant amount each game, the Value10,20, and 30 all ended up w/ b/w 1800,1200,1600 dollars, respectively
      if you "LetItRide", the Value10,20, and 30 ended up with : 361,2200, and >20,000. This shows that the LetItRide is highly volatile but potentially very lucrative.  
