# semgraph-hoax-id
Evaluating Semantic Graph and Temporal Modeling for Indonesian Hoax Detection on Twitter/X using Temporal Graph Neural Network (TGNN).

# Evaluating Semantic Graph and Temporal Modeling for Indonesian Hoax Detection on Twitter

Code and replication files for the paper submitted to the International Journal of Advances in Data and Information Systems (IJADIS).

## Data
The tweets come from IDNHoaxCorpus [repository URL], which is not redistributed here.
Please download it from the original repository and cite the corpus papers listed there.
Tweet times are obtained by decoding the Snowflake ID in each tweet URL:
timestamp_ms = (tweet_id >> 22) + 1288834974657

## How to reproduce
1. Download the original dataset and place it where the notebook expects it.
2. Run notebook/final-ab-revision-v7.ipynb from top to bottom (five seeds: 42, 123, 2024, 7, 999).
3. Compare the notebook output with the files in replication/.

## Files in replication/
- nodes_split_snapshot.csv: node_id, posting time, label (0 = valid, 1 = hoax), split, snapshot
- edges_topk_threshold.csv: older node, newer node, cosine similarity (threshold 0.572, K = 4)
- config.json: settings used for the experiments
- versions.txt: library versions
