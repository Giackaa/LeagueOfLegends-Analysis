## League Data Project

Welcome to the League Data Project repository! This project documents my journey and challenges as I explore and analyze data related to League of Legends, a game I am passionate about. From raw data exploration to advanced analytics, this repository will grow with insights, experiments, and solutions I discover along the way.

-----
## About the Project

This project investigates the relationship between **support vision scores** and **jungler performance** in *League of Legends*.  
The data was scraped from the **Riot Games API**, cleaned and transformed using **Excel**, **Power Query**, and **MySQL**, and analyzed visually with **Tableau**.

The primary question:  
> 💡 *Does a support’s vision control correlate with their jungler’s effectiveness — specifically pick kills and gold advantage?*

## 🧑‍💻 Tech Stack
| Tool | Purpose |
|------|----------|
| 🐍 **Python** | Data scraping from Riot API |
| 📊 **Excel / Power Query** | Data cleaning, joining, and transformation |
| 🗄️ **MySQL** | Database management for large datasets |
| 📈 **Tableau** | Visual analysis and percentiles-based performance comparison |
---
## Data Trimming and Cleaning

### 🧽 Cleaning & Transformation
- Removed one-sided matches (<14 min).
- Grouped by `gameId` to summarize each game.
- Used Power Query to:
  - Join Champion ID ↔ Champion Name datasets.
  - Unpivot → join → pivot champion tables.
  - Union all champion tables from a folder into a single dataset.


-----
## Excel Analysis

### 🧩 Data Organization
- Sorted players into **teams** and **roles**.
- Verified data using **game length** and **win/loss**.
- Filtered out:
  - Non-jungler / non-support roles.
  - Games under **1200 seconds (20 min)** — excluded early surrenders, AFKs, or smurfs.

### ⚖️ Gold Comparison
- Grouped players by `gameId`.
- Calculated **min** and **max** gold values for each match.
- Excluded matches with **gold differences > 100 gold/min** (imbalanced games).

### 👁️ Vision vs. Pick Kills
- Divided **vision scores** into 5 percentiles (0–20, 20–40, 40–60, 60–80, 80–100).
- Compared jungler **pick kills** under:
  - High-vision supports (80–100%)
  - Low-vision supports (0–20%)
- Scatter charts were too messy → replaced with **percentile-based aggregation**.
- Compartmentalized **pick kills** into percentiles to reveal clearer correlations.

### 🔍 Advanced Formulas
Used **Power Query** and **complex Excel logic** to:
- Merge jungler + support data into single rows (`gameId` + team side).
- Use `OFFSET`, nested `IF`, and dynamic `INDEX` functions to pull data directly from pivot tables.
- Avoid static value tables that break when refreshing pivots.

-----
## Tableau Visualization 
### Approach
1. **Percentile-Based Evaluation**
   - Used **percentiles** to evaluate jungler performance in games with **low vs. high support ward placements** within specific time slots.
   - Since each time slot has different distributions, percentiles were calculated separately per slot.

2. **LOD (Level of Detail) Expressions**
   - Utilized **LOD expressions** to calculate fixed **75th** and **25th percentiles** for each time slot.
   - This ensured consistent comparison across varying game lengths.

3. **Categorization**
   - Created **calculated fields** using `IF` statements to categorize performance:
     - `"Above 75th"`
     - `"Below 25th"`
     - `"Other"`

4. **Data Filtering**
   - Excluded games with durations **beyond 3000 seconds** due to significantly lower sample sizes.
   - This step helps **avoid statistical illusions** and maintain data integrity.
-----
## Key Insights
- Those who place more wards than 75% of other players increase their jungler’s gold earning by an average of 618 gold vs. 162 gold for those who has killed more wards
- Vision control beyond 20 minutes becomes a game-wide advantage, not just lane-specific.  
- Killing more wards increases an extra 0.42 to the jungler's gank kills, while placing more wards is an extra 0.93, more than 2x more efficient than killing more wards.
- In fostering a better performative environment for the jungler, I would recommend a support to focus on placing more wards around the map rather than seeking to kill more wards.
---

## Future Enhancements
- 🔁 Automate data scraping via **scheduled Python tasks** (`cron`, `apscheduler`, or `schedule`).  
- 🧮 Expand the dataset with **rank-tier breakdowns** (Platinum → Challenger).  
- 🤖 Apply **machine-learning models** (e.g., regression) to predict jungle performance from vision metrics.  
- 💾 Create a **Streamlit dashboard** for real-time visualization and interactive filtering.
-----
Feedback and Collaboration

I am open to suggestions and feedback as I refine my methods and learn more about data analysis and League of Legends. If you want to collaborate or discuss ideas, feel free to reach out!
