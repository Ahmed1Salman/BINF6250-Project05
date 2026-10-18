# Introduction
The application of the **Smith-Waterman Algorithm** transformed Computational Biology and Bioinformatics. It established a mathematical framework to find the optimal `local sequence alignment` between two nucleotide or protein sequence, identifying pairs of segments across two long sequences that has maximum local similarity. The algorithm isolates highly conserved local regions or functional domains while ignoring non-conserved flanking regions.

The program has Key Features & Biological Significance:
* **Dynamic Programming Matrix**: Computes local alignment scores cell-by-cell by evaluating matches, mismatches, and insertion/deletion (indel) gap penalties.
* **Zero Threshold Option ("Free Start")**: Includes a minimum score threshold of `0` in the recurrence relation , preventing cumulative negative scores and allowing local alignments to start cleanly anywhere in the matrix.
* **Traceback Procedure**: Begins at the **global maximum score element** in the matrix (marking the end of the alignment) and steps backward along direction pointers until hitting a cell score of **`0`** (marking the start of the alignment).
* **Arbitrary Indel Handling**: Flexible scoring scheme accommodating match rewards, mismatch penalties, and gap penalties

# Pseudocode
```
FUNCTION CAL_SCORE(matrix, seq1, seq2, i, j, match, mismatch, gap):
    # COMPARE SEQUENCE CHARACTERS
        IF seq1[i - 1] == seq2[j -1]
            match_score = match
        ELSE
            match_score =  mismatch
 
    # CALCULA PATH SCORES GROM THE PREDECESSORS
        diag_score = matrix[i - 1, j - 1] + match_score
        up_score   = matrix[i - 1, j] + gap
        left_score = matrix[i, j - 1] + gap
 
    # COMPUTE SCORE EITH THE ZERO THRESHOLD
        score = MAX(0, diag_score, up_score, left_score)
 
    # RECORD TRACEBACK DIRECTION
        IF score == 0
            move = (0) END
        ELSE IF score == diag_score
            move =  (1) DIAG  
        ELSE IF score == up_score
            move =  (2) UP    
        ELSE
            move = (3) LEFT  
 
        RETURN score, move
 
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
    maximum_position = list of tuples
 
    # Forward Sweep: Fill score and traceback matrices cell-by-cell
    FOR i FROM 1 TO RANGE(n) DO
        FOR j FROM 1 TO m DO
            (score, move) = CAL_SCORE(score_matrix, seq1, seq2, i, j, match, mismatch, gap)
            score_matrix[i][j] = score
            traceback_matrix[i][j] = move
 
            // Track global maximum cell position
            IF score > max_score
                max_score = score
                maximum_position = (i, j)
            ELIF position_score == mac_value
            maximun_positoin.append(current_position)
    
 
    # Backward Sweep: Reconstruct local alignment from the maximum score position
    FOR pos IN MAXIMUM POSITION
    (aligned_seq1, aligned_seq2) = TRACEBACK(seq1, seq2, traceback_matrix, maximum_position)
 
    RETURN aligned_seq1, aligned_seq2, score_matrix
 
```
 
# Successes
Description of the team's learning points
 
# Struggles
Description of the stumbling blocks the team experienced
 
# Personal Reflections
## Group Leader
Group leader's reflection on the project
 
## Member - Graziano Peregrino  
Other members' reflections on the project
 
# Generative AI Appendix
 
Description of which generative AI was used and its version.
- NotebookLM 2.0 and Gemini 4 Argon
 
Updated the book and articles to notebookml and start asking about details of dynamic programming chapter.
 
The entire prompt that was used to generate the content.
- I need some help to understand dynamic programming and the walk of the nodes in the matrix.
- Can you show me a numerical example of filling a grid?
- I want to understand why the algorithm chooses the path with highest weight.
- Can you explain the diagonal reasoning?
- Can you explain dynamic programming in an arbitrary DAG?
- How can I calculate the weight of the diagonal?
- Can you explain the topological order on the dressing challenge problem?
- How would I modify the alignment graph to solve the gap penalty issue?
- How do affine gap penalties work?
- Can you provide some explanation on this The Four Option Recurrence Relation?
- How could we construct an alignment without storing any backtracking pointers?
 
An explanation of how it was used (e.g., to generate ideas).
- I used it as a tool to learn the concepts described on the chapter, asking for further clarification on the material and extra examples.
 
A justification for why generative AI was used.
- Sometimes just reading a concept and formula is not enough for me to have a grasp on the material, so I used it as an additional source to lern about dynamic programming.

# Reference
-Compeau, P., & Pevzner, P. (2015). Bioinformatics Algorithms: An Active Learning Approach (2nd ed., Vol. 1)
. Active Learning Publishers, LLC
