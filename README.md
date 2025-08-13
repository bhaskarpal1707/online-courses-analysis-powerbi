# 📊 Online Courses Analysis Dashboard

## 🏆 Insights-Driven Exploration of the Online Learning Market
---

# Dashboard

---

## 📑 Table of Contents:
1. [Overview](#Overview)
2. [Business Problem](#Business-Problem)
3. [Dataset](#Dataset)
4. [Tools & Technologies](#Tools-&-Technologies)
5. [Project Structure](#Project-Structure)
6. [Data Cleaning & Preparation](#Data-Cleaning-&-Preparation)
7. [DAX Queries](#Dax-Queries)
8. [Custom Columns](#Custom-Columns)
9. [Research Questions & Key Findings](#Research-Questions--Key-Findings)
10. [Final Recommendations](#Final-Recommendations)
11. [Author & Contact](#Author--Contact)

---

## 📌 Overview
This project analyzes around **10,000 online courses** sourced from multiple platforms like **Coursera, Udacity, Simplilearn, and FutureLearn**, providing deep insights into **category trends, skill demand, instructor performance, and engagement patterns**.  
The Power BI dashboard built from this dataset offers **data-driven strategic recommendations** for content development and learner engagement optimization.
The goal was to uncover actionable insights into **course categories, viewership patterns, skills demand, language preferences, instructor quality, and content strategies** for the EdTech sector.

---

## 💼 Business Problem
With the rapid growth of online education, understanding **what drives learner engagement, which skills are in demand, and how to optimize course offerings** is crucial for competitive advantage.  
This analysis aims to:
- Examine the distribution of course types across categories to uncover trends and insights, enabling the client to strategically determine which course types to launch in specific categories for maximum impact and alignment with learner demand, also count the number of courses by category and sub-category.
- Calculate the average number of views for each category, sub-category, and language to provide insights into viewer engagement patterns and inform strategic content development.
- Identify the most commonly taught skills in today's educational landscape based on the data given based on category to ensure course offerings remain relevant and aligned with current job market demands.
- What is the distribution of various Languages  in which a particular course is  created?
- Determine the language preferences for each category based on viewer preferences, so that clients can optimise course accessibility and better align content with audience demand. Clients only want to analyse this data for the top 5 categories based on user preferences.
- Investigate the relationship between the availability of subtitles and the number of views for courses to determine how subtitle options may impact viewer engagement and accessibility.
- Identify the top three instructors for each category and subcategory based on ratings   to highlight educators who consistently deliver high-quality content and effectively engage learners so that they can be approached by your client to make content for them and make this visual as static.
- Examine the relationship between course duration and the number of views to understand how the length of a course may influence viewer engagement and preferences for each category and sub-category, if course duration has a month (in each month only 60 hours of content ) and for flexible schedules make the timing as 200 hours.
- In the context of recorded lectures, we need to investigate whether the variety of skills offered within each category and subcategory has a measurable impact on viewership.

---

## 📂 Dataset
**Source:** Kaggle — *Online Courses Dataset*
**Link:** https://www.kaggle.com/datasets/khaledatef1/online-courses

**About:**
**Size:** ~10,000 rows  
**Format:** CSV  
**Features:** Course title, platform, category, skills, instructors, duration, ratings, number of viewers, subtitles, etc.

---

## 🛠 Tools & Technologies
- **Power BI** → Dashboard creation & visualization
- **Microsoft Power Query** → Data cleaning & transformation
- **DAX (Data Analysis Expressions)** → Measures and calculated columns for analysis 
- **CSV Data Source** → Dataset storage

---

## 📁 Project Structure
Online-Courses-Analysis/
│── data/
│ └── Online_Courses.csv
│── dashboard/
│ └── Online Courses Analysis Dashboard.pbix
│── README.md


---

## 🧹 Data Cleaning & Preparation
Performed in **Power Query**:
- Removed errors
- Removed duplicates
- Removed blank rows
- Renamed columns
- Filtered rows
- Removed unnecessary columns
- Extracted text before delimiter
- Changed data types
- Replaced values
- Added custom calculated columns

---

## 📊 DAX Queries
```DAX
-- Rank Category by Average Views
Rank_category_by_average_views = 
IF(
    RANKX(
        ALL(Online_Courses[Category]),
        CALCULATE(AVERAGE(Online_Courses[Number of viewers]))
    ) < 6,
    CALCULATE(AVERAGE(Online_Courses[Number of viewers])),
    BLANK()
)

-- Instructor Rating
Instructors_Rating = 
IF(
    RANKX(
        ALL(Teachers[Instructors]),
        CALCULATE(AVERAGE(Teachers[Rating]))
    ) <= 3,
    CALCULATE(AVERAGE(Teachers[Rating])),
    BLANK()
)

```
---
# 🧩 Custom Columns
```
-- Count of Skills Provided
Text.Length([Skills]) - Text.Length(Text.Replace([Skills], ",", ""))

-- Duration in Hours
if Text.Contains(Text.Lower([Duration]), "month") then 
    Number.FromText(Text.Select([Duration], {"0".."9"})) * 60
else if Text.Contains(Text.Lower([Duration]), "hour") then
    Number.FromText(Text.Select([Duration], {"0".."9"}))
else if Text.Contains(Text.Lower([Duration]), "minute") then 
    Number.FromText(Text.Select([Duration], {"0".."9"})) / 60
else 
    200

-- New Subtitle Language Count
List.Count(Text.Split([Subtitle Languages], ","))
```
---

## 🔍 Research Questions & Key Findings

### **Category Distribution & Course Types**
- **Findings:**
  - Computer Science dominates, followed by Business and Data Science.
  - Specializations are the most popular course type.
  - Professional Certificates are strong in tech categories.
- **Recommendations:**
  - Expand Specializations in high-demand areas.
  - Introduce Professional Certificates in emerging tech fields.
  - Prioritize Computer Science & Business for new courses.

---

### **Viewer Engagement Patterns**
- **Findings:**
  - Business & Computer Science have the highest average views.
  - English courses vastly outperform other languages.
  - Data Science subcategories show high engagement.
- **Recommendations:**
  - Focus on English-first content.
  - Invest heavily in Business & Computer Science content creation.
  - Develop Data Science Specializations.

---

### **In-Demand Skills**
- **Findings:**
  - **Computer Science:** Python, JavaScript, Web Development.
  - **Business:** Project Management, Leadership, Marketing.
  - **Data Science:** Machine Learning, Data Analysis, Python.
  - **Information Technology:** Cloud Computing, Cybersecurity.
- **Recommendations:**
  - Promote Python across categories.
  - Expand Leadership & Project Management content.
  - Build comprehensive Cloud Computing curricula.

---

### **Language Preferences**
- **Findings:**
  - English dominates (~80–85% of all courses).
  - Spanish & French are secondary languages.
  - Minimal representation of other languages.

---

### **Subtitle Impact**
- **Findings:**
  - Courses with subtitles have **15–25% higher views**.
  - Multi-language subtitles significantly boost global engagement.

---

### **Top Instructor Insights**
- **Findings:**
  - **Computer Science:** Instructors with 4.8+ ratings and strong programming expertise.
  - **Business:** Industry experts with high engagement.
  - **Data Science:** Blend of academic credentials and practical application skills.

---

### **Duration vs. Engagement**
- **Findings:**
  - Optimal engagement for courses **3–6 months** in duration.
  - **200-hour flexible courses** work well for professionals.
  - Short courses are best for skill-specific training.

---

### **Skills Variety**
- **Findings:**
  - Broader skill offerings lead to higher overall viewership.
  - Cross-functional skill combinations perform exceptionally well.

 ---
 ## 📌 Final Recommendations

### **Immediate (0–3 months)**
- Expand Computer Science & Business offerings.
- Implement subtitle strategy.
- Partner with top-rated instructors.

### **Medium-term (3–12 months)**
- Develop multilingual strategy for top categories.
- Introduce modular 3–6 month course structures.
- Launch cross-functional skill programs.

### **Long-term (12+ months)**
- Lead in Specialization-format courses.
- Build a Professional Certificate ecosystem.
- Create AI-powered personalized learning pathways.

---

## 👤 Author & Contact
**Bhaskar Pal**  
Aspiring Data Analyst  
📧 **Email:** [bhaskarpal.official@gmail.com](mailto:bhaskarpal.official@gmail.com)  
🔗 **LinkedIn:** [Bhaskar Pal](https://www.linkedin.com/in/bhaskar-pal-2k02/)  






