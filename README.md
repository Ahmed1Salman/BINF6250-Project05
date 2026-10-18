# BINF6250
```
FUNCTION CAL_SCORE(matrix, seq1, seq2, i, j, match, mismatch, gap):
    # COMPARE SEQUENCE CHARACTERS
        IF seq1[1 - 1] == seq2[j -1]
            match_score = match
        ELSE
            match_score = match
 
    # CALCULA PATH SCORES GROM THE PREDECESSORS
        diag_score = matrix[i - 1, j - 1] + match_score
        up_score   = matrix[i - 1, j] + gap
        left_score = matrix[i, j - 1] + gap
 
    # COMPUTE SCORE EITH THE ZERO THRESHOLD
        score = MAX(0, diag_score, up_score, left_score)
 
    # RECORD TRACEBACK DIRECTION
        IF score == 0
            move = END   (0)
        ELSE IF score == diag_score
            move = DIAG  (1)
        ELSE IF score == up_score
            move = UP    (2)
        ELSE
            move = LEFT  (3)
 
        RETURN score, move
```
