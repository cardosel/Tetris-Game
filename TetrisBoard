
public class TetrisBoard
{
	
	//boolean array to construct board (instance)
	private boolean[][] board;
	
	
	//number of rows of the board variable
	private static final int TETRIS_ROWS = 18;
	
	
	//number of columns in board variable
	private static final int TETRIS_COL = 10;
	
	//variable for calling current piece
	private TetrisPiece currentPiece;
	
	//variable for locating where current piece is located on grid
	private int[] currentGridPosition;

	//Constructor
	public TetrisBoard()
	{
		//sets up the board
		initBoard();
		//initialize the position of the grid point
		initGridPoint();
		//add a new piece to the game
		addNewPiece();
	}

	//Initialize an int array of length two to track rows and columns
	private void initGridPoint()
	{
		//initialize
		currentGridPosition = new int[2];
		//keep the position of the current piece at (0, 3)
		currentGridPosition[0] = 0;
		currentGridPosition[1] = 3;

	}



	//Add new random tetris piece
	//place at position (0,3)
	public void addNewPiece()
	{
		//variable for random number
		double random = Math.random()*7;

		//assign a tetris piece to the current piece if random # falls in one of these categories
		if (random < 1)
		 	currentPiece = new TetrisL1();
		else if (random < 2)
		 	currentPiece = new TetrisL2();
		else if (random < 3)
		 	currentPiece = new TetrisS1();
		else if (random < 4)
		 	currentPiece = new TetrisS2();
		else if (random < 5)
		 	currentPiece = new TetrisSquare();
		else if (random < 6)
		 	currentPiece = new TetrisStick();
		else
		 	currentPiece = new TetrisT();
		
		// reset the grid location
		initGridPoint();
	}
	
	//Refresh the display to show where the new pieces landed
	//using the gridPoint values and rotation values 

	public void	pieceLanded()
	{
 		//go through all rows and columns less than size 4 (tetris size)
		for (int i = 0; i < 4; i++){
			for (int j = 0; j < 4; j++){
				//if a piece is found
				if (currentPiece.isFilled(currentPiece.getPieceRotation(), i, j))
				{
					// give it a row position
					int row = currentGridPosition[0] + i;
					
					// give it a col postion
					int col = currentGridPosition[1] + j;
					
					// set the new value to true
					board[row][col] = true;
				}
			}
		}
	}

// check if piece can move down, if so move it down. 
	
	public boolean dropDown()
	{
		//assign a new variable to focus on row position of new piece
		
		int newRowPoint = currentGridPosition[0] + 1;
		
		// if it can drop down, 
		if (availablePoint(currentPiece, currentPiece.getPieceRotation(), newRowPoint, currentGridPosition[1]))
		{
			//drop the piece down
			currentGridPosition[0] = newRowPoint;
			
			//return true
			return true;
		}
		else
			//return false if piece can't move
			return false;
	}

	//Checks if shift left is possible.

	public boolean shiftLeft()
	{
		//assign new var to focus on col point
		
		int newColumnPoint = currentGridPosition[1] - 1;
		// can we shift left?
		
		if (availablePoint(currentPiece, currentPiece.getPieceRotation(), currentGridPosition[0], newColumnPoint))
		{
			// if so shift it to the left.
			currentGridPosition[1] = newColumnPoint;
			//return true
			return true;
		}
		else
			//return if piece can't shift left
			return false;
	}
	
	//Checks if shift right is possible.
	public boolean shiftRight()
	{
		//assign new var to focus on col point
		int newColumnPoint = currentGridPosition[1] + 1;
		// can we shift right?
		if (availablePoint(currentPiece, currentPiece.getPieceRotation(), currentGridPosition[0], newColumnPoint))
		{
			// if so shift it to the left.
			currentGridPosition[1] = newColumnPoint;
			//return true
			return true;
		}
		else
			//return if piece can't shift left
			return false;
	}

	//Checks if we can rotate counter clockwise.
	public boolean rotateCounter()
	{
		//assign new var to focus on rotation point.
		int currentRotation = currentPiece.getPieceRotation();
		//if rotation is at 0
		if (currentRotation == 0)
			//rotate the piece by 270 degrees.
			currentRotation = 3;
		// if not possible
		else
			//move back 90 degrees
			currentRotation -= 1;

		//can we move counter clockwise?
		if (availablePoint(currentPiece, currentRotation, currentGridPosition[0], currentGridPosition[1]))
		{
			//then rotate the piece
			currentPiece.rotateClock();
			//return true
			return true;
		}
		else
			//return false if we can't rotate
			return false;
	}

	//Checks if we can rotate clockwise.
	public boolean rotateCW()
	{
		//assign new var to focus on rotation point.
		
		int currentRotation = currentPiece.getPieceRotation();
		//if rotation is at 0
		
		if (currentRotation == 3)
			// if so, rotate 270 degrees
			currentRotation = 0;
		//if not, rotate 0 degrees
		else
			//move the piece back 90 degrees
			currentRotation += 1;

		//can we rotate clockwise?
		if (availablePoint(currentPiece, currentRotation, currentGridPosition[0], currentGridPosition[1]))
		{
			//if so, then rotate.
			currentPiece.rotateClock();
			//return true
			return true;
		}
		else
			//return false if we cannot rotate.
			return false;
	}
	
	//Checks if the grid position is available using rotation points
	// detects any blocking by a piece or edge
	
	private boolean	isBlocked(TetrisPiece piece, int rot, int gridRow, int gridCol)
	{
		//loop through all rows/col less than size of tetris piece
		
		for (int i = 0; i < 4; i++){
			for (int j = 0; j < 4; j++){
				//if piece touches index in board
				
				if (piece.isFilled(rot, i, j) && board[gridRow+i][gridCol+j]){
					System.out.println("Incorrect move");
					//return true
					return true;
				}
			}
		}
		return false;
	}

	//check if piece is out of bounds other wise piece would fall of board
	
	private boolean	isOutofBound(TetrisPiece piece, int rot, int gridRow, int gridCol)
	{
		//loop through all row/col less than size 4
		for (int i = 0; i < 4; i++){
			for (int j = 0; j < 4; j++){
				int row = gridRow + i;
				int col = gridCol + j;
				//if piece is found
				if(piece.isFilled(rot, i, j)){
					
					//if the point is located outside the board
					if ((row < 0) || (row >= TETRIS_ROWS) || (col < 0) || (col >=TETRIS_COL)){
						System.out.println("Incorrect move");
						//then the piece is outside the board
						return true;
					}
				}
			}
		}

		return false;
	}


	//checks with rotation points if the space is available
	private boolean	availablePoint(TetrisPiece piece, int rot, int gridRow, int gridCol)
	{
		//is there blocking or out of board?
		if (isOutofBound(piece, rot, gridRow, gridCol) || isBlocked(piece, rot, gridRow, gridCol))
			//the it's unavailable
			return false;
		//else
		else
			//the space is available
			return true;
	}

	//checks if there is a block  exists in the space
	public boolean blockExists(int row, int col)
	{
		// get the rotation point
		int rot = currentPiece.getPieceRotation();

		// loop through all the row/col less than size 4
		for (int i = 0; i < 4; i++){
			for (int j = 0; j < 4; j++){
				
				// if within the range of i and j, check if there is an x
				 if(currentPiece.isFilled(rot, i, j) && (currentGridPosition[0] + i == row) && (currentGridPosition[1] + j == col))
					{
						// return the block's point
						return true;
					}
			}
		} 
		//return that point's value                                                                                                                                                                                                                         
		return (board[row][col]);
	} 

	//Determines if any lines are filled
	public int numFullLines()
	{
		//var to number of filled lines
		int filledLines = 0;
		//loop through all the rows
		for(int i = 0; i < TETRIS_ROWS; i++){
			//if the line is filled,
			if (fullLine(i))
			{
				//increment by 1
				filledLines ++;
				//remove line
				removeLine(i);
			}
		}
		//return the number of lines
		return filledLines;

	}

	//Check if there an unavailable line in row
	public boolean fullLine(int row)
	{
		//loop through all the columns
		for (int j = 0; j < TETRIS_COL; j++){
			//if there is any false value in the given row
			if (!board[row][j])
				//the line is not full
				return false;
		}
		//else, the line is full
		return true;
	}
	
	//delete the line in the model
	private void removeLine(int row)
	{
		//loop through the array
		for(int i = TETRIS_ROWS - 1; i > 0; i--){
			for(int j = TETRIS_COL - 1; j >= 0; j--){
				//shift points so they are a row higher
				board[i][j] = board[i-1][j];
			}
		}
	}
	
	//method to get board
	public boolean[][] getBoard() 
	{
		return board;
	}

	//getter method to get the current grid position
	public int[] getCurrentGridPosition() 
	{
		return currentGridPosition;
	}
	
	// initializes the board
		private void initBoard()
		{
			//initialize the board
			board = new boolean[TETRIS_ROWS][TETRIS_COL];
			// initialize the contents of the board
			for ( int i = 0; i < TETRIS_ROWS; i++){
			    for (int j = 0; j < TETRIS_COL; j++){
					//set value to false
					board[i][j] = false;
				}
			}
		} 

	//getter method
	public TetrisPiece getCurrentPiece() 
	{
		return currentPiece;
	}

	//getter method 
	public int getNumCols()
	{
		return TETRIS_COL;
	}

	//getter method 
	public int getNumRows()
	{
		return TETRIS_ROWS;
	}
}
