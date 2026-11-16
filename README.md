# Product Recommender (Apache Mahout)

A small user-based collaborative-filtering recommender in Java. It reads user ratings from a CSV file, finds users with similar taste using Pearson correlation, and recommends products the target user has not rated yet.

## How it works

1. `FileDataModel` loads `data/dataset.csv`. Each line is `userID,itemID,rating`.
2. `PearsonCorrelationSimilarity` measures how similar two users' ratings are.
3. `NearestNUserNeighborhood` picks the 2 most similar users for the target user.
4. `GenericUserBasedRecommender` predicts ratings for unseen items from those neighbours and returns the top results for user `1`.

```
.
├── data/dataset.csv                                   # 5 users, 20 ratings (toy data)
├── src/main/java/com/recommender/
│   ├── ProductRecommender.java                        # recommends top 3 items for user 1
│   └── UserBasedRecommenderDemo.java                  # same pipeline, top 2 items
└── pom.xml                                            # Maven build (Mahout 0.9)
```

## Run it

Requires JDK 11+ and Maven. Run from the project root so `data/dataset.csv` is found.

```bash
mvn compile
mvn exec:java
```

To run the other class: `mvn exec:java -Dexec.mainClass=com.recommender.UserBasedRecommenderDemo`

## Honest scope

This is a learning prototype, not a production recommender:

- The dataset is tiny (5 users, 20 ratings), so results are only for demonstrating the pipeline.
- There is no evaluation yet (for example RMSE or precision@k on a train/test split).
- The target user, neighbourhood size and number of results are hard-coded.

## Next steps

- Swap in a real dataset such as MovieLens and add a train/test evaluation (`RecommenderEvaluator`).
- Compare Pearson with other similarity measures (cosine, Euclidean) and item-based recommenders.
- Take the user ID from the command line.
