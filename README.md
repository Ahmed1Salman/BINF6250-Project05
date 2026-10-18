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
```
