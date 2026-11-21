### EX3 Implementation of GSP Algorithm In Python
### DATE: 20-11-2026 
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>
### Program:

```
python
from collections import defaultdict
from itertools import combinations

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
    c = defaultdict(int)
    for seq in dataset:
        flat_seq = []
        for itemset in seq:
            if isinstance(itemset, str):
                flat_seq.extend(itemset.split(','))
            else:flat_seq.extend(itemset)

        # count each combination once per sequence
        for comb in set(combinations(sorted(flat_seq), k)):
            c[comb] += 1

    res = {}
    for item, support in c.items():
        if support >= min_support:
            res[item] = support
    return res

# Function to perform GSP algorithm
def gsp(dataset, min_support):
    k = 1
    fp = defaultdict(int)
    while True:
        c = generate_candidates(dataset, k)
        if not c:
            break
        fp.update(c)
        k += 1
    return fp

# Example dataset
top_wear_data = [
    [["a"],["b"],["c"],["b","e"],["c"],["f"],["g"],["a","b","e"]],[["a"],["d"],["b","c"],["c"],["f","g"],["c","h"]],
    [["b"],["c"],["a","d"],["e"],["b"],["f"],["c","d","f","g","h"]],
    [["c"],["e","c"],["e","h"]] 
]

min_support = 3

# Run GSP
top_wear_result = gsp(top_wear_data, min_support)

# ---------- TABULAR OUTPUT ----------
patterns_by_length = defaultdict(list)

for pattern, support in top_wear_result.items():
    patterns_by_length[len(pattern)].append((pattern, support))

print("\nFrequent Sequential Patterns \n")

for length in sorted(patterns_by_length):
    print(f"{length}-Length Patterns")
    print("-" * 30)
    print(f"{'Pattern':20} {'Support'}")
    print("-" * 30)
    for pattern, support in patterns_by_length[length]:
        print(f"{str(pattern):20} {support}")
    print()


```
### Output:

<img width="651" height="225" alt="546524680-6f0d60a2-b84f-4ca7-b654-1402074288fa" src="https://github.com/user-attachments/assets/fed14c34-6191-4af3-a1ec-6fa6a676dedf" />
<img width="631" height="292" alt="546524736-ef878b33-fff8-4c17-9b03-6f4ced2bad46" src="https://github.com/user-attachments/assets/0d9c1d9b-2328-43a6-a46a-8e188014e381" />
<img width="800" height="338" alt="546524786-b3bf4c79-72ed-4e36-b165-2db63f07262e" src="https://github.com/user-attachments/assets/0fddf54d-46d7-4186-9e1c-69a91a86b5de" />
<img width="638" height="260" alt="546524829-a77aa4c2-5986-47a8-b03a-24736bb714e9" src="https://github.com/user-attachments/assets/2ae954c5-6d7c-43d6-8f47-030233e1af38" />
<img width="814" height="256" alt="546524876-1de01880-48a9-488d-a45a-8f42c5dd5666" src="https://github.com/user-attachments/assets/c9fa9458-7bce-4276-aa51-586d70d2d004" />



### Visualization:
```
import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize frequent sequential patterns for each category using a line plot
visualize_patterns_line(top_wear_result, 'Top Wear')

```
### Output:

<img width="1126" height="558" alt="546525414-193c11c1-487d-4eb1-890b-455dbdf7befd" src="https://github.com/user-attachments/assets/7d791252-e9a2-4ae1-977b-a9df49f1e9e3" />


### Result:

Thus , the implementation of GSP Algorithm in Python Program is Successfully.
