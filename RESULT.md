# Evaluation Results & Findings

## Comparison Table

| Query | Keyword rank | Semantic rank |
|---|---|---|
| my redis cache keeps showing old data | 8 | 1 |
| how do I add semantic search to a table I already have | miss | 2 |
| redis or memcached for caching | 1 | 2 |
| why did my query get slower after I added an index | miss | 1 |
| what does ACID actually guarantee | 2 | 1 |
| how do I keep my postgres online while changing the schema | 6 | 3 |
| my background jobs stop after every deploy | miss | 2 |
| how do I let my database accept more writes per second | 4 | 1 |
| sql or nosql for a new product | 1 | 3 |
| why does my redis memory keep climbing | miss | 2 |
| **Summary** | **MRR 0.30 · Recall@10 0.60** | **MRR 0.67 · Recall@10 1.00** |

## Findings & Interpretation

Overall, semantic search is clearly the superior retrieval system across both metrics, achieving an MRR of 0.67 compared to keyword search's 0.30, and reaching a perfect Recall@10 of 1.00 compared to keyword search's 0.60. Keyword search only won on queries featuring specific, canonical technical names and direct technology comparisons, namely "redis or memcached for caching" (rank 1 vs 2) and "sql or nosql for a new product" (rank 1 vs 3), where exact lexical terminology matches the target documents. In contrast, semantic search dominated on natural-language problem descriptions and symptom-based questions such as "why did my query get slower after I added an index" and "my background jobs stop after every deploy", where keyword search produced outright misses due to vocabulary mismatch. A production engineering team should still keep the keyword search system around because the two systems excel at complementary query distributions, making a hybrid search architecture (combining lexical BM25 with vector embeddings via Reciprocal Rank Fusion) more effective and resilient than either approach on its own.
