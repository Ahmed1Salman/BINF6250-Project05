# Introduction
This project explores the fundamental principles of genome assembly using short DNA sequencing reads . The goal is to implement a simple overlap-based assembler that identifies overlapping reads, merges them into longer sequences, and continues the process until no additional merges are possible. The resulting sequences, or contigs, are then analyzed to evaluate how well the reads cover the assembled genome.The project also examines how the choice of overlap length (k) affects assembly accuracy. A small k can lead to incorrect overlaps between unrelated reads, while a large k can cause genuine overlaps to be missed. It also explores the fundamentals of object oriented programming in creating the De Bruin graph that follows a eularian walk.

# Pseudocode

```
def add_edge(self, left, right):
  append right to graph[left]

def remove_edge(self, left, right):
  self.graph[left].remove(right)

def build_graph_from_reads(self, reads, k):
  for each read in reads:
            for i from 0 to len(read) − k:
                kmer  = read[i : i+k]
                left  = kmer[0 : k−1] # drop last base for prefix
                right = kmer[1 : k]   # drop first base for suffix
                add_edge(left, right)

def eulerian_walk(self, node, graph, seed=None, tour=None):
  tour = []
        while graph[node] still has edges:
            next_node = pick a random neighbor from graph[node]
            remove_edge(node, next_node) #consume edge                 
            tour.extend(eulerian_walk(next_node, graph)) #recurse 
        tour.append(node) # append on the way back out
        return tour # deepest node was added first, want to reverse it at the end

def assemble_contigs(self, seed=None):
  seed the RNG once
  graph = a copy of self.graph
  compute indegree of every node

  contigs = []
  #Start from ideal nodes which have more outgoing than incoming edges to start path
  for node in nodes where out > in:
      while graph[node] has edges:
          tour = reverse(eulerian_walk(node, graph))
          contigs.append(tour_to_sequence(tour))
  #Anything left over is a cycle, start anywhere that still has edges
  for node in all nodes:
      while graph[node] has edges:
          tour = reverse(eulerian_walk(node, graph))
          contigs.append(tour_to_sequence(tour))
  return contigs

def tour_to_sequence(self, tour):
  if tour is empty: return ""
  seq = [tour[0]]
  for node in tour[1:]:
      seq.append(node[-1])
  return "".join(seq)

def get_assembly_stats(self, contigs):
  lengths = sorted(len(c) for c in contigs, descending)
  num_contigs, total_length, longest = lengths[0], shortest = lengths[-1], mean
  n50: walk down the sorted lengths keeping a running sum;
      the first length where running sum >= total_length / 2 is the N50
  (handle empty contig case by returning zeros)


def write_fasta(self, contigs, filename):
  for i, contig in enumerate(contigs, 1):
    write ">contig_i length=N"
    write the sequence 


```

# Successes
Description of the team's learning points

# Struggles
Our main struggles as a team were finding a time that worked for everyone given our schedules, and figuring out how to optimize the code for the yeast dataset. The toy dataset took a very short time to run and it outputted the contig as expected. The yeast dataset took 81 minutes to run compared to the expected 6-7 minutes, and finding ways to optimize the code was a struggle for us. 

# Personal Reflections
## Group Leader - Bessie
Group leader's reflection on the project

## Yulia
This project was a challenge since we all had different schedules and it was difficult to work collaboratively as much. Bessie and Abigail had elected to meet first to brainstorm and start some work on code, and after I had finished the code based on their work. Bessie also wrote out her version of the code too, so we chatted on Teams to compare the codes and see how we could make the yeast dataset more efficient. It took my version 81 minutes for it to run. It took the longest to run at the building debrujin graph step. Assembling contigs took the second longest amount of time. I do suspect my memory could be a factor here, as I did not run it on an HPC. Marcus did mention it should take 6-7 minutes to run, but I wonder if he ran it on the HPC. I think the main bottleneck here was in the for loop. Adding in print statements was helpful for me to visualize the progress of the datasets while they ran so it would not sit in silence.

## Other member
Other members' reflections on the project

# Generative AI Appendix
Claude was used to modify pseudocode logic, code syntax for eulerian_walk, assemble_contigs, tour_to_sequence, get_assembly_stats. It was also used to answer questions about how recursion works. 
