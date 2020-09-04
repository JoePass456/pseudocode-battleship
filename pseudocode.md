Battleship AI Opponent (USER vs BOT):

-Using 1990 Milton Bradley ruleset (versions do differ.  For example, the ship list in the 2002 release is slightly different)


Set 1990SHIPS.dat   //This will be a premade file that will contain the ship info for the 1990 MB version of Battleship containing:
                    //              A, 5, Aircraft Carrier
                    //              B, 4, Battleship
                    //              C, 3, Cruiser
                    //              S, 3, Submarine
                    //              D, 2, Destroyer
                    
--------------------------------------------------------------------------------------------------------------------------------------

START PROGRAM

Init SHIPLIST.dat                           // This by default will be 1990SHIPS.dat, but *COULD* be set by an input variable

Init BOTMAP                                 // BOTMAP file will be a string of 100 characters representing the 10x10 grid

Init USERLOG.dat and BOTLOG.dat             // LOGS will be data files that store the TURN, X, Y, and HIT variables 

Init USERSCR and BOTSCR                     // These init at 0 points and will be used to determine the game winner
                                    
Init WINSCR                                 // This will be set in the program as the condition for win,
                                            //    (in the 1990 version the number will be set to 17)
                                    
Init TURN = 1                               // This will keep track of the current turn number and be recorded in the LOG files

Init TURNMARK                               // This is a turn marker and will alternate from U to B to determine who's turn it is

Init SHIPABBR, SHIPSIZE, and SHIPNAME       // This will be used to pull data from the SHIPLIST.dat file 

Init X and Y                                // These will be the coordinates of each shot of the USER or BOT and will be recorded in the LOG.dat

Init RESULT                                 // After each shot is declared, this will either be computed or computed and will be used to enter into the
                                            //    USERLOG or BOTLOG
Init FOLLOWUP                               // This will be a TRUE or FALSE set by the followUpShot function            
                                       

FUNCTION setBotMap                          // This will read the SHIPS.dat file and randomly assign each ship a location
  output: BOTMAP                            //    !! Using the data, this program will use RNG (using X and Y) to place one ship in a starting location,
  output: WINSCR                            //    use RNG to determine orientation, and then use SHIPSIZE to determine final location.
                                            //    IF ship is (a) out of bounds or (b) overlapping a previaously set ship, THEN program will
                                            //    RETURN to !! and REPEAT UNTIL all ships (in this case five) are in legal positions. 
                                            // This will also add up ship sizes to Compute WINSCR
                                            // NOTE: This *COULD* be greatly simplified by using preset patterns, however this would hamper the 
END                                         //    replayability of the game.

INPUT "Who will go first?": TURNMARK        // Rules simply state "Choose a player to go first", therefore this program allows the USER to make
                                            //    this determination.  This will Set the TURNMARK to either U or B
                                            
----------------------------------------------------------------------------------------------------------------------------------------------------------------                                            
                                            
IF USERSCR and BOTSCR < WINSCR THEN {       // If either players acheives the WINSCR, then they have won and the program will exit this loop

  
  IF TURNMARK = U     // Begins USER turn
  
    INPUT "Enter your shot!": X,Y           // The user enters the X and Y variables for his shot both must be 1 - 10 ELSE REPEAT
    
    FUNCTION computeHit (X,Y,BOTMAP)        // Cross references the coordinates of the shot with the BOTMAP and logs either "miss!" or 
      output:RESULT
    FUNCTION logResult(USERLOG,X,Y,RESULT)             // "Hit!".  If hit it will log which ship was hit and add a point to the USERSCR.  It will also log 
                                            // the X,Y and RESULT(as HIT) in the USERLOG file as.
  ELSE   
 
  
  IF FOLLOWUP = TRUE THEN                   // By default, the BOT will use RND applied to X and Y to make a shot, however, if the last shot
     FUNCTION followUpShot                  //   was a hit then it will continue to take shots based on an algorithm and RNG to keep shooting
                                            //   until the ship is sunk.  IF this shot is already logged, it will REPEAT.  Once ship is sunk it
                                            //   will reassign FOLLOWUP to FALSE
  
  ELSE          // Ends USER turn, begin BOT turn
  
  
    FUNCTION takeShot                       // If not shooting a followUpShot, this function uses RNG to select X and Y for shot.  If this
      output: X, Y                          // shot has already been logged it will REPEAT until shot is a new coordinate
      
    LOG "Incoming shot at coordinates" X, Y
  END                                        
  
  INPUT "Did shot hit?": RESULT             // The user will input if the a ship was hit and which ship it was.
  
  END  
  FUNCTION logResult(BOTLOG,X,Y,RESULT)    //  function updates the BOTLOG  
  
  END IF        //  Ends BOT turn
                                            
)  
------------------------------------------------------------------------------------------------------------------------------------------------------------

ELSE

IF USERSCR = WINSCR LOG "Congradulations, you won!"

ELSE

LOG "Sorry, your fleet has been destroyed!  Better luck next time!"

END PROGRAM
