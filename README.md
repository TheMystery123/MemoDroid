# MemoDroid

## 🚀 Introduction

LLM-based GUI agents are increasingly used for automated app testing by interpreting GUI screenshots and generating interactions. However, existing agents lack long-term memory and treat each app as a cold start, missing the opportunity to learn from prior sessions.

MemoDroid addresses this by introducing a **three-layer memory mechanism**:
- **Episodic Memory**: Captures functional interaction traces (screenshots, actions, transition graphs).
- **Reflective Memory**: Summarizes redundant or issue-prone behaviors into natural language.
- **Strategic Memory**: Synthesizes high-level exploration strategies across apps or domains.

These memory layers are **dynamically retrieved** during testing and injected into LLM prompts to:
- Reuse successful past behaviors,
- Avoid ineffective or redundant actions,
- Prioritize bug-prone paths.

---

## 🧠 Architecture

![MemoDroid Overview](./assets/overview.png)

MemoDroid is a lightweight plugin and works **on top of any LLM-based GUI testing framework**. Memory is triggered:
- At cold start (strategic memory),
- During testing stagnation (reflective memory),
- At functional transitions (episodic memory).

Each memory item is encoded using **CLIP-style vision-text encoders** and **graph embeddings**, allowing efficient retrieval by similarity.

---

## 📦 Features

- ✅ LLM-based multimodal understanding (screenshots + GUI hierarchy).
- 🧠 Three-level memory mechanism (episodic, reflective, strategic).
- 🔁 Dynamic memory retrieval and injection.
- 📈 Significant improvement in activity/code coverage and bug detection.
- 🧪 Supports version evolution & platform transfer (Android → Web).

---

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


---

## 🧪 How to Use

### Environment Setup

#### 1. Android Studio Setup
1. Download Android Studio from [official website](https://developer.android.com/studio)
2. Install Android Studio following the installation wizard
3. Launch Android Studio and complete the initial setup

#### 2. Android Virtual Device (AVD) Setup
1. Open Android Studio
2. Click "Tools" > "Device Manager" > "Create Virtual Device"
3. Select a device definition (e.g., Pixel 2)
4. Select a system image:
   - Choose x86 Images for better performance
   - Recommended: API 30 (Android 11.0) or higher
   - Download the system image if not available
5. Configure AVD settings:
   - Set device name
   - Adjust RAM size (recommended: 2GB or more)
   - Set internal storage (recommended: 2GB or more)
6. Click "Finish" to create the AVD

#### 3. Physical Device Setup (Alternative)
1. Enable Developer Options on your Android device:
   - Go to Settings > About Phone
   - Tap "Build Number" 7 times
2. Enable USB debugging in Developer Options
3. Connect device via USB
4. Allow USB debugging on device when prompted

### Setup and Installation

1. Install required dependencies:
```bash
pip install -r requirements.txt
```

2. Configure the application:
   - Set up API keys in the configuration
   - Adjust processor settings as needed


### Bug Collection System
```bash
# Generate start URLs
python collect_bugs/gen_start_urls.py

# Run F-Droid spider
scrapy runspider collect_bugs/fdroid_spider.py

# Collect GitHub issues
python collect_bugs/github_spider.py

# Analyze data
python collect_bugs/merge_and_analysis.py
```

### Running the Demo to generate memory
```bash
python demo.py
```

## Data Availability
The complete dataset of 60 apps used in our experiments is publicly available at: [Google Drive](https://drive.google.com/drive/folders/1x7sDGJ4R_MmR57kVGi64IWekAAxxqbUV?usp=sharing)