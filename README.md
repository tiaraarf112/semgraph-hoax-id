# semgraph-hoax-id

## Evaluating Semantic Graph and Temporal Modeling for Indonesian Hoax Detection on Twitter

Code and replication files for the paper submitted to the International Journal of Advances in Data and Information Systems (IJADIS). The paper is a controlled comparison of three models for Indonesian hoax detection: an MLP on frozen IndoBERT embeddings, a Static GCN, and a TGNN with per-tweet memory. Two controls with the TGNN architecture are also included, one that reads neighbor text without memory and one that uses no neighbors.

## Data

The tweets come from IDNHoaxCorpus
[https://github.com/9uz/IDNHoaxCorpus/blob/main/dataset/datasetUMPOHoax.csv](https://github.com/9uz/IDNHoaxCorpus/blob/main/dataset/datasetUMPOHoax.csv),
which is not redistributed here. Please download it from the original repository and cite the corpus papers listed there:

- R. Arifin, G. N. Syaifuddiin, Desriyanti, Z. U. Rosyidin, and G. A. Buntoro, "A Highly Accurate Internet-Based Fake Information Detection Tool for Indonesian Twitter," Informatica, vol. 46, no. 9, pp. 25-30, 2022, doi: 10.31449/INF.V46I9.4416.
- G. N. Syaifuddiin et al., "Hoax Identification of Indonesian Tweeters Using Ensemble Classifier," Journal of Information Systems and Telecommunication, no. 11(2), pp. 94-101, 2023, doi: 10.52547/JIST.33532.11.42.94.

Tweets labeled "?" are removed. Timestamps are obtained by decoding the Snowflake ID in each tweet URL:

`timestamp_ms = (tweet_id >> 22) + 1288834974657`

## How to reproduce

1. Download the original dataset (link above).
2. Open Kaggle, create a new notebook, and upload `notebook/final-revision-v7.ipynb`. Add the dataset CSV through "Add Input". The notebook finds the CSV automatically under `/kaggle/input/`.
3. Turn on a GPU. The reported results come from a GPU (CUDA) run.
4. Run the notebook from top to bottom (five seeds: 42, 123, 2024, 7, 999). Outputs are written to `/kaggle/working/artifacts`.
5. Compare the notebook output with the files in `replication/`.

## Where the paper results come from

| Paper item | Notebook section |
|---|---|
| Graph construction, homophily (Table 5) | Sections 9, 10 |
| TGNN and its two controls | Section 15B |
| Table 3 and Table 4 | Sections 17B, 18, 35 |
| Figure 7 (confusion matrices, mean of five seeds) | Section 18B |
| Figure 6 (validation curves) | Section 19 |
| Neighbor composition, graph structure | Section 22 |
| Sensitivity to K and threshold | Section 26 |
| Longer patience (30) as a robustness check | Section 30C |
| Files in `replication/` | Section 34 |

## Files in replication/

- `nodes_split_snapshot.csv`: node_id, waktu_posting (the timestamp decoded from the tweet ID), label (0 = valid, 1 = hoax), split, snapshot. It does not contain tweet text.
- `edges_topk_threshold.csv`: older node, newer node, cosine similarity (threshold 0.572, K = 4)
- `config.json`: settings used for the experiments
- `versions.txt`: library versions

## Notes

- Results were produced on a GPU. A CPU run gives slightly different values.
- `SELF_LOOP_WEIGHT_TGNN` in `config.json` is a leftover from an earlier version and is not used by the reported TGNN.
- The split is chronological (70/15/15) and the graph only has edges from older to newer tweets.

## License

MIT (see `LICENSE`). The license covers the code in this repository, not the IDNHoaxCorpus data.

## Citation

Citation details will be added after publication.
