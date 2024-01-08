# Analyzing Students' Mental Health
## Part of DataCamp's Data Analyst in SQL Track

***

## Project Description:

Does going to university in a different country affect your mental health? A Japanese international university surveyed its students in 2018 and published a study the following year that was approved by several ethical and regulatory boards.

The study found that international students have a higher risk of mental health difficulties than the general population, and that social connectedness (belonging to a social group) and acculturative stress (stress associated with joining a new culture) are predictive of depression.

Explore the "students" data using PostgreSQL to find out if you would come to a similar conclusion for international students and see if the length of stay is a contributing factor.

## Data Description:

| Field Name    | Description                                      |
| ------------- | ------------------------------------------------ |
| `inter_dom`     | Types of students (international or domestic)   |
| `japanese_cate` | Japanese language proficiency                    |
| `english_cate`  | English language proficiency                     |
| `academic`      | Current academic level (undergraduate or graduate) |
| `age`           | Current age of student                           |
| `stay`          | Current length of stay in years                  |
| `todep`         | Total score of depression (PHQ-9 test)           |
| `tosc`          | Total score of social connectedness (SCS test)   |
| `toas`          | Total score of acculturative stress (ASISS test) |

## Analysis Process

1. Save the CSV file as "students"
```sql
# Query 1: 
SELECT * 
FROM 'students.csv';
```
![Screen Shot 2024-01-07 at 19 07 46](https://github.com/kivatmojo/datacamp_sql/assets/137433466/0457a084-9fa1-476a-9a49-5a666f3089a9)

2. Counting the data
```sql
# Query 2: Counting the number of records
SELECT COUNT(*) AS total_records
FROM students;
```
![Screen Shot 2024-01-07 at 19 08 03](https://github.com/kivatmojo/datacamp_sql/assets/137433466/7c9c9073-13ec-4b70-8c27-0c9de71e00e8)


```sql
# Query 3: Counting the number of records that are not null
SELECT COUNT(*) AS total_records_clean
FROM students
WHERE inter_dom IS NOT NULL;
```
![Screen Shot 2024-01-07 at 19 08 11](https://github.com/kivatmojo/datacamp_sql/assets/137433466/2f21fc2b-fee4-436d-a985-74f111f7f02f)


```sql
# Query 4: Counting the number of international students
SELECT COUNT(*) AS total_inter
FROM students
WHERE inter_dom = 'Inter';
```
![Screen Shot 2024-01-07 at 19 08 18](https://github.com/kivatmojo/datacamp_sql/assets/137433466/fa1faa8c-6ee9-4ef1-b5b0-e878a3c420a4)


3. Exploring and understanding the data
```sql
# Query 5: Statistics of desired mental health metrics, grouped by student status
SELECT inter_dom, 
	MIN(todep) AS min_dep, MAX(todep) AS max_dep, AVG(todep) AS avg_dep, 
	MIN(tosc) AS min_sc, MAX(tosc) AS max_sc, AVG(tosc) AS avg_sc, 
	MIN(toas) AS min_as, MAX(toas) AS max_as, AVG(toas) AS avg_as
FROM students
WHERE inter_dom IS NOT NULL
GROUP BY inter_dom;
```
![Screen Shot 2024-01-07 at 19 08 29](https://github.com/kivatmojo/datacamp_sql/assets/137433466/af090e16-1667-469a-8833-a2c388f103a8)


```sql
# Query 6: Finding a correlation between length of stay and mental health metrics
SELECT stay, 
	ROUND(AVG(todep),2) AS avg_dep, 
	ROUND(AVG(tosc),2) AS avg_sc, 
	ROUND(AVG(toas),2) AS avg_as
FROM students
WHERE inter_dom = 'Inter'
GROUP BY stay
ORDER BY stay DESC;  
```
![Screen Shot 2024-01-07 at 19 08 38](https://github.com/kivatmojo/datacamp_sql/assets/137433466/9b0eb208-0159-4823-8549-6fc1f4b8b8e8)

4. Findings
- 

