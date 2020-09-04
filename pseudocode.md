Battleship AI Opponent (USER vs BOT):
*Using 1990 Milton Bradley ruleset
*versions do differ.  For example, the ship list in the 2002 release is slightly different


Set 1990SHIPS.dat   //This will be a premade file that will contain the ship info for the 1990 MB version of Battleship containing:
                    //              A, 5, Aircraft Carrier
                    //              B, 4, Battleship
                    //              C, 3, Cruiser
                    //              S, 3, Submarine
                    //              D, 2, Destroyer
                    
--------------------------------------------------------------------------------------------------------------------------------------

START 

Init USERMAP.dat and BOTMAP.dat             // MAP and GRID files will be a string of 100 characters representing the 10x10 grid

Init USERGRID.dat and BOTGRID.dat           //      Initiated maps and grids will be blank; in this case a string of of "0"s  

Init USERLOG.dat and BOTLOG.dat             // LOGS will be data files that store the TURN, X, Y, and HIT$ variables 

Init USERSCR and BOTSCR                     // These init at 0 points and will be used to determine the game winner
                                    
Init WINSCR                                 // This will be set in the program as the condition for win,
                                            //      (in the 1990 version the number will be set to 17)
                                    
Init TURN = 1                               // This will keep track of the current turn number and be recorded in the LOG files

Init TURNMARK                               // This is a turn marker and will alternate from U to B to determine who's turn it is

Init SHIPABBR, SHIPSIZE, and SHIPNAME       // This will be used to pull data from the *SHIPS.dat file  

PROGRAM setbotmap                           // This will read the *SHIPS.dat file and randomly assign each ship a legal location
                                            // (*) Using the data, this program will use RNG to place one ship in a starting location,
                                            // use RNG to determine orientation, and then use SHIPSIZE to determine final location.
                                            // IF ship is (a) out of bounds or (b) overlapping a previaously set ship, THEN program will
                                            // reset to (*



