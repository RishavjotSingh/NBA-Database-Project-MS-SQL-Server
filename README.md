## About the Project

This project uses Microsoft SQL Server for the database. This project is a Database project for an NBA analyst, and allows an analyst to get meaningful and useful information that they might be interested in for 2021-2022 season using the list of commands provided. All query descriptions are provided beside the commands themselves. 

## Creating the Database

A SQL file named "nbaData.sql" is provided. The database can be created by running this SQL file on your Microsoft (MS) SQL Server. An easy way to do this is to make a connection to your MS SQL Server on an easy-to-use platform like Visual Studio Code (any platform can be used for this purpose). And after making a connection with your server, this SQL file can be run which would create the entire database.

## How to Run 

In the "auth.cfg" file you have to provide the JDBC connection link to your MS SQL Server using which the Java program will be able to connect to your database to be able to run the queries and provide the required data. This link has to be put after "msSqlServerJdbcConnectionLink=", for example I used my University's SQL Server to create my database and auth.cfg file looked like:

```msSqlServerJdbcConnectionLink=jdbc:sqlserver://HostName:PortNumber;database=DatabaseName;user=Username;password=Password;encrypt=false;trustServerCertificate=false;loginTimeout=30;```

You can provide JDBC connection link to your database created on your MS SQL Server. After providing the link in the auth.cfg file, you can compile and run the project using the command ```make run```.

## How to use

Once built and ran, it is very intuitive and easy to use. The program will ask the user to insert a value from the following output:

Type "t" for team related commands.
Type "p" for player related commands.
Type "o" for other commands.
Type "exit" to exit the program.

The queries/commands are divided into three categories to make it easy for the user. Copy the commands on left and paste as input to run.

The user can choose any of the three commands to get a list or queries or type "exit" at anytime to quit the project.

## Queries and Explanation

### Team related queries

Entering "t" will give the user a list of team related queries, see below. They can choose from any of the queries.
There is a short description provided in front of each of the commands.

```
=========================================================================================================================================================
loc                                - List all NBA Teams, their abbreviation, location and arenas they play at.
MostPtsAtLocation <location>       - Enter first few letters of location or "City, State" format.
                                     Most points by a player at a location over the season, and their team name. Use "l" command for all locations.
GameDescription                    - Get a list of all game Ids, game dates, home teams and away teams.
WhoWon <game_id>                   - Enter game_id to see who won a particular game.
                                     Use "GameDescription" command to look up game_id's or enter team abbreviation for all their home games.
TeamEfficiencyRanking              - Rank teams by Points Per Possession, Used to find the best offensive teams, anything above "1.1" is considered good.
MostWinsOverPeriod <st> <en>       - Enter two dates between 2021-10-18 and 2022-04-11 in YYYY-MM-DD format. Ranks teams by wins in that period of time.
                                     To measure teams performance in chunks, is used for a number of reasons; injuries, coaching change, etc.
FreeThrow                          - Top 5 Free throw shooting teams.
RankTeams                          - League Standings.
MostFoulingTeam                    - Teams that foul the most.
============================================================================================================================================================================
```
### Their Significance 

loc: Even for a full-time NBA analyst, it can be hard to remember all the teams and the cities they play in.

MostPtsAtLocation: This is a trivial query but can be used by an analyst when writing about NBA destinations.

GameDescription: Helper query, gives reference to game dates, id's and the teams, helps during scheduling or planning or looking up stuff by game ID.

WhoWon: Gives the date and who won a particular game, but most of the time, the user will search with team abbrev and get results for all home games.
The query uses aggregate functions, group by and inner query.

TeamEfficiencyRanking: This is how NBA analysts gauge good offensive teams.
The query uses aggregate functions and group by.

MostWinsOverPeriod: When looking up gradual improvements or regression by teams; an analyst can view their performance or period of time. Can be used measure teams performance in chunks, is used for a number of reasons; injuries, coaching change, etc.
The query uses aggregate functions and group by.

FreeThrow: It is an important stat in the NBA, it's literally "Free", the best offenses usually have the highest free throw attempts.

RankTeams: Gives standings team standings for the season.

MostFoulingTeam: Gives teams that have fouled the most over the season.

### Team related queries

Entering "p" will give the user a list of player related queries, see below. They can choose from any of the queries.
There is a short description provided in front of each of the commands.

```
===========================================================================================================================================================
MostPtsAtHome                      - Who scored the highest points at a home game for each team.
                                     Returns multiple players if they had the same high score at home.
MostPtsByAwayPlayer                - Who scored the highest points at an away game for each team.
                                     Returns multiple players if they had the same high score away from home.
PlayerPlayedAtAllLocations         - Players who played at all NBA arenas over the season.
Top10BestPlusMinusAvg              - Top 10 players highest average plus-minus.
                                     It measures how much a team scored when the player was on the floor.
Top25MostEffPlayers                - Top 25 Most efficient players this season. Important stat, used to find the best offensive players.
                                     abbreviated as "PER" Player efficiency rating, usually the player with highest PER is the MVP.
                                     It is derived by a simple formula: (PTS + REB + AST + STL + BLK − Missed FG − Missed FT - TO) / GP.
MostEffEachTeam                    - This stat gives the "best" player on each team. 
                                     It is derived by a simple formula: (PTS + REB + AST + STL + BLK − Missed FG − Missed FT - TO) / GP.
BestUnder25                        - Top 10 Best young; up and coming players under 25 in the NBA.
PlayedAllGames                     - Players who played all games in the NBA
BestInTheGame                      - Top 15 Best players in the game ranked by points per game, used for all star / all NBA selection.
playerStatsInd <name>              - Provide either exact player names or some letters in the name.
                                     Important because NBA Analysts are always looking up players stats.
MostFoulingPlayer                  - Players That foul the most.
===========================================================================================================================================================
```

MostPtsAtHome: Which home players had the highest points for each team. Used by analyst to find the top scorer at home.
The query uses aggregate functions, group by and inner query.

MostPtsByAwayPlayer: Which home players had the highest points for each location. Used by analyst to find best away players.
The query uses aggregate functions, group by and inner query.

PlayerPlayedAtAllLocations: Usually use by analysts to find the most travelled players.
A division query uses inner query. Took quite long to figure out.

Top10BestPlusMinusAvg: Plus minus stat gives the analyst a way to find the players that contribute to winning.
Uses aggregate functions.

Top25MostEffPlayers: Important stat, used to find the best offensive players.
abbreviated as "PER" Player efficiency rating, usually the player with highest PER is the MVP.
It is derived by a simple formula: (PTS + REB + AST + STL + BLK − Missed FG − Missed FT - TO) / GP.

MostEffEachTeam: Used to find the best offensive players on each team.
abbreviated as "PER" Player efficiency rating. Was quite complex to figure out, uses inner query
aggregate functions and group by.

BestUnder25: Gives the best young players, Analysts look at this to structure contracts.

PlayedAllGames: Players who played all games, played by the team.
This is quite complex query with three inner queries, took a very long time to figure out def interesting.

playerStatsInd: Very important to an NBA analysts as they look up player stats all the time.

MostFoulingPlayer: players who fouled the most.

### Other Queries

Entering "o" will give the user a list of other queries, see below. They can choose from any of the queries.
There is a short description provided in front of each of the commands.

```
===========================================================================================================================================================
ImprovedCoach                      - Coaches with better winning percentage this season compared to their career.
MostGamesOfficiated                - Referees who officiated the most number of games.
OverTimeGames                      - Returns all overtime games.
HomeReferee                        - Referees who favoured home teams.
MultipleCoaches                    - Teams that were coached by multiple coaches.
WhoReferredWhat <st>               - Provide game_id for a particular game or Team Abbrev to see who refereed all their home games.
                                     Use "GameDescription" command to look up game_id's or enter team abbreviation.
============================================================================================================================================================
```

### Their Significance 

ImprovedCoach: Important to an analyst because improved coaches usually get better contracts.

MostGamesOfficiated: Most active referees.

HomeReferee: Referees who favoured home teams. This is something Analysts look at quite consistently.

OverTimeGames: Return all overtime games.

MultipleCoaches: Teams coached by multiple coaches in a season. Consistently look up by Analysts.

WhoReferredWhat: Look up query used by analysts.