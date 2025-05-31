# Experiment Results

## RQ1: Effectiveness Evaluation
Our evaluation on 30 real-world Android apps across 15 categories demonstrates that MemoDroid significantly enhances GUI testing performance across all five baseline approaches:

| Baseline          | Activity Coverage Improvement | Code Coverage Improvement | Bug Detection Improvement |
|-------------------|-------------------------------|---------------------------|---------------------------|
| GPTDroid          | ↑79%                          | ↑81%                      | ↑194%                     |
| DroidAgent        | ↑96%                          | ↑89%                      | ↑198%                     |
| AUITestAgent      | ↑86%                          | ↑86%                      | ↑57%                      |
| VisionDroid       | ↑88%                          | ↑87%                      | ↑71%                      |
| Guardian          | ↑93%                          | ↑97%                      | ↑72%                      |

Key findings:
- Episodic memory enables effective action replication
- Reflective memory helps identify crash-prone behaviors
- Strategic memory provides high-level exploration guidance

## RQ2: Ablation Study
Removing any memory layer causes significant performance degradation:

| Memory Layer Removed | Avg. Coverage Drop | Avg. Bug Detection Drop |
|----------------------|--------------------|-------------------------|
| Episodic Memory      | 23-26%             | 14-24%                  |
| Reflective Memory    | 29-38%             | 19-39%                  |
| Strategic Memory     | 15-22%             | 11-19%                  |

Reflective memory shows the strongest individual contribution to performance.

## RQ3: Memory Evolving Effect
Testing performance improves progressively as memory pool expands:

- Initial 5 apps provide sufficient diversity for generalization
- Performance gains continue through 60-app memory pool
- VisionDroid+MemoDroid achieves 0.71 activity coverage (+73% from baseline)

## RQ4: Practical Usefulness
In large-scale evaluation on 200 popular apps:
- Detected **49 previously unknown bugs** in 47 apps
- **35 bugs fixed** and **14 confirmed** by developers
- 7 bugs were only detectable with MemoDroid augmentation

Example developer feedback:  
*"This bug affects core functionality and was hindering users' ability..."* - Wallet App maintainer

## Cross-Version & Cross-Platform Testing
- **Version Evolution**: Maintains effectiveness across 5 versions of Wallet app (v2.0-v5.0)
- **Platform Transfer**: Android memory improves web testing (7 vs 3 bugs detected in SeeAct)

## Data Availability
The complete dataset of 60 apps used in our experiments is publicly available at: [Google Drive](https://drive.google.com/drive/folders/1x7sDGJ4R_MmR57kVGi64IWekAAxxqbUV?usp=sharing)



