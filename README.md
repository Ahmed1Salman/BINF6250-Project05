# BINF6250
```
FUNCTION TRACEBACK(seq1, seq2, traceback_matrix, maximum_position):
 
    # Initialize lists:
    aligned_seq1 = empty list
    aligned_seq2 = empty list
 
    (current_row, current_col) = maximum_position
 
    WHILE current_row > 0 AND current_col > 0:
 
        current_move = traceback_matrix[current_row][current_col]
 
        IF current_move == END (0):
            BREAK
 
        ELSE IF current_move == DIAG (1)
            Append seq1[current_row - 1] TO aligned_seq1
            Append seq2[current_col - 1] TO aligned_seq2
 
            current_row = current_row - 1
            current_col = current_col - 1
 
        ELSE IF current_move == UP (2)
            Append seq1[current_row - 1] TO aligned_seq1
            Append "-" to aligned_seq2
 
            current_row = current_row - 1
 
        ELSE IF current_move == LEFT (3)
            Append "-" TO aligned_seq1
            Append seq2[current_col - 1] TO aligned_seq2
 
            current_col = current_col - 1
      
    
 
    # Reverse lists since traceback constructs the alignment backward
 
    aligned_seq1 = REVERSE(aligned_seq1) AND JOIN TO STRING
    aligned_seq2 = REVERSE(aligned_seq2) AND JOIN TO STRING
 
    RETURN aligned_seq1, aligned_seq2

FUNCTION SMITH_WATERMAN(seq1, seq2, match = +1, mismatch = -1, gap = -1):
 
    n = LENGTH(seq1)
    m = LENGTH(seq2)
 
    # Initialize scoring matrix and traceback matrix with zeros
    Initialize score_matrix of size (n + 1) × (m + 1) filled with 0s
    Initialize traceback_matrix of size (n + 1) × (m + 1) filled with 0s
 
    max_score = 0
    maximum_position = (0, 0)
 
    # Forward Sweep: Fill score and traceback matrices cell-by-cell
    FOR i FROM 1 TO n DO
        FOR j FROM 1 TO m DO
            (score, move) = CAL_SCORE(score_matrix, seq1, seq2, i, j, match, mismatch, gap)
            score_matrix[i][j] = score
            traceback_matrix[i][j] = move
 
            // Track global maximum cell position
            IF score > max_score THEN
                max_score = score
                maximum_position = (i, j)
    
 
    # Backward Sweep: Reconstruct local alignment from the maximum score position
    (aligned_seq1, aligned_seq2) = TRACEBACK(seq1, seq2, traceback_matrix, maximum_position)
 
    RETURN aligned_seq1, aligned_seq2, score_matrix
```
