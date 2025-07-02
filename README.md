# STUDENT'S MENTAL HEALTH ANALYSIS

### Table of Contents
[Introduction](#introduction)

[Objectives](#objectives)

[Basis](#basis)

[Project Strategy](#project-strategy)

[Feature Engineering](#feature-engineering)

[Visualization and Key Findings](#visualization-and-key-findings)

[Statistical Analyses of Student Data](#statistical-analyses-of-student-data)



### Introduction
---

Mental health has become an increasingly important topic in educational institutions, especially among university students who face academic pressures, social expectations, and personal challenges. This report explores the mental health status of students based on various factors, including gender, CGPA, year of study, course of study, and marital status.

The dataset used for this analysis includes key indicators such as depression, anxiety, and panic attacks, along with demographic and academic details. The objective of this study is to identify trends, uncover risk factors, and provide insights into the prevalence of mental health issues among students. By analyzing the data, visualizing key patterns, and drawing meaningful conclusions, this report aims to contribute to better mental health awareness and support strategies within academic environments.

Additionally, this study provides data-driven recommendations to help universities, educators, and policymakers implement targeted interventions and create a healthier learning environment for students. The findings are presented using various visualizations and statistical insights, offering a comprehensive understanding of the relationship between academic life and mental well-being.

---
### Objectives
**WHAT DO WE NEED TO ANSWER IN THIS REPORT?**
---
To provide a comprehensive and data-driven analysis, this report aims to answer the following critical questions:
- What is the prevalence of mental health issues among students, and how does it vary by gender?
- How does academic performance (CGPA) relate to mental health issues?
- Are certain years of study more associated with mental health struggles?
- Does a student’s course of study influence their likelihood of experiencing mental health issues?
- What are the key insights from the demographic and statistical analysis of the students surveyed?

---
### Basis
--
This Data set was collected by a survey conducted by Google forms from university student to examine their current academic situation and mental health. All the data was based on Malaysia and collected from IIUM (International Islamic University Malaysia).
I downloaded this dataset from https://www.kaggle.com/datasets/shariful07/student-mental-health/data in CSV (Comma Separated Values) format and it has the following column headers;

- Timestamp – a combination of the date and time taken of survey by students.
- Choose your gender – Male or Female
- Age – Age of students
- What is your course?
- Your current year of Study
- What is your CGPA?
- Marital status
- Do you have Depression?
- Do you have Anxiety?
- Do you have Panic attacks?
- Did you seek any specialist for treatment?

---

**Courses and their abbreviations.**
- BIT: Business Information Technology
- Pendidikan Islam: Teachings and principles of Islam
- BCS: Bachelor of Computer Science
- KENMS: The Kulliyyah of Economics and Management Sciences
- ENM: Environmental and Natural Resource Management
- KOE: Kulliyyah of Engineering
- KIRKHS: Kulliyyah of Islamic Revealed Knowledge and Human Sciences
- Usuluddin: Also known as Usul al-Din, is an Arabic term that means "principles of religion" or "fundamentals of faith”.
- TAASL: Teaching Arabic as a Second Language
- ALA: Applied Liberal Arts
- BENL, TESL: Basic English in The Native Language (English as Second Language)
- CTS: Certified Technology Specialist.
- MHSC: Master of Health Science.
- Malcom, communication: Malaysia Communication.
- KOP: Kulliyyah of Pharmacy.
- Fiqh fatwa, Figh: Islamic jurisprudence (Fiqh) and the issuance of legal rulings (Fatwa) based on Islamic principles and teachings.
- Engine, Engin, KOE = Engineering (Which means that these values should be joined to each other)
- Econs: Economics.

---

Let's divide them into faculties. I think some of the professions might be the same, but just wrote in different way, so I clustered them to be used for data analysis:

--

IT:
- Business Information Technology
- Bachelor of Computer Science
- Internet Technology
- Certified Technology Specialist

--

Engineering:
•	Engineers

--

Law:
- Law
- Islamic jurisprudence and the issuance of legal rulings based on Islamic principles.

--

Medicine:
- Biomedical science
- Master of Health Science
- Biotechnology

--

Nursing;
•	Radiography

--

Economics and management:
- Economics
- The Kulliyyah of Economics and Management Sciences
- Human Resources
- Accounting
- Banking Studies
- Business Administration
- Mathematics

--

Religion, sociology and ethnography and psychology (RSEP):
- Islamic Education
- Teachings and principles of Islam
- Principles of religion
- Principles of religion" or "fundamentals of faith
- Kulliyyah of Islamic Revealed Knowledge and Human Sciences
- Psychology
- Communication

--

Environment:
- Environmental and Natural Resource Management
- Marine Science

--

Linguistics:
- Arabic as a Second Language
- English as a Second Language

--

Art:
•	Applied Art Studies.

---

### Project Strategy
--

With Microsoft Excel, I did all the cleaning, visualizations, and analysis. There was not much cleaning, but these were the few things I did.
- Under “Your Current Year of Study” column, there was inconsistencies of the word year, Year, so I made everything to be in a sentence case format (Year).
- One of the cells in the “Age” column (cell name C45) was blank so I took the mean (Average) of all ages and manually typed in the result there. The mean of the “Age” column is 20.53 and so I approximated it to be 21. I used the mean of all ages because it maintains the data integrity, avoid biases, and preserves the trend of other student ages.
- Under “What is your course?” there were responses like “Engin, Engine, and Engineering. I replaced “Engin and Engine for Engineering” because they all mean the same thing.

--

After doing this, the dataset became clean for visualization and analysis. Hence
- There were no duplicates.
- There were no unnecessary spaces.
- The datatypes for each column were aligned with their respective columns.


---
### Feature Engineering
---

This is the process of selecting, transforming, and creating new features from existing data to improve the performance and activity of machine learning models. In this case, there are no machine learning models.

1.	I employed feature engineering for the columns; Do you have depression? Do you have anxiety? Do you have panic attack? because while trying to visualize these columns to show the number of male and female who had these mental issues, Excel took the total numbers of male and female genders which will give a false impression of the visualization. In here, I called in the function; =IF([@[Do you have Depression?]]="Yes",1,0) for depression, =IF([@[Do you have Anxiety?]]="Yes",1,0), and =IF([@[Do you have panic attack?]]="Yes",1,0) to;
- Converts Yes/No answers into numerical values (1 and 0), Yes for 1 and No for 0 making it easier to sum or analyze.
- Help with data visualization (e.g., creating charts or calculating percentages).

So, I did feature engineering for Do you have depression? as “Depression (Numeric)” Do you have anxiety? as “Anxiety Numeric” and Do you have panic attack? as “Panic Attack (Numeric).


2.	HOW THE CGPA MIDPOINT WAS DERIVED
In the dataset, CGPA values were presented as ranges (e.g., "3.00 - 3.49"). To perform meaningful statistical analysis and visualizations, we needed to convert these ranges into single numerical values. This was achieved by calculating the midpoint of each CGPA range using the following Excel formula:

--

Formula Used:
=(--LEFT(F2,FIND(" - ",F2)-1) + --MID(F2,FIND(" - ",F2)+3,LEN(F2))) / 2

--

**How the Formula Works:**
Extracting the Lower Bound: LEFT(F2,FIND(" - ",F2)-1)
This extracts the first number before the hyphen ("-").

Extracting the Upper Bound: MID(F2,FIND(" - ",F2)+3,LEN(F2))
This extracts the second number after the hyphen.

Converting to Numerical Values:
The -- before the LEFT and MID functions ensure that the extracted values are converted from text to numbers.

Calculating the Midpoint:
The formula then sums the two extracted values and divides by 2 to get the midpoint.
Example Calculation:
For a CGPA range of "3.00 - 3.49", the formula calculates:

(3.00+3.49)/2=3.245
(3.00+3.49)/2=3.245

This method was applied across all CGPA values, allowing for statistical analysis such as descriptive statistics, scatter plots, and bar charts.

---
### Visualization and Key Findings
**VISUALIZATION AND KEY FINDINGS**
A.	Gender Distribution: I created pivot tables and chart that showed the gender distributions having more females than male students. With a total number of 101 students, 75 are female students and 26 are male students.

---

**B.	Mental Health Issues by Gender:**
a.	Higher Prevalence of Mental Health Issues in Females
- The number of females experiencing Depression, Anxiety, and Panic Attacks is significantly higher than males (29 vs. 6 for Depression, 24 vs. 10 for Anxiety, and 25 vs. 8 for Panic Attacks).
- This suggests that female students might be more affected by mental health challenges compared to males.

--

b.	Anxiety is the Most Common Mental Health Issue Among Males
- 10 males report Anxiety, compared to 6 with Depression and 8 with Panic Attacks.
- This indicates that anxiety might be a more pressing issue among male students.

--

c.	Depression is the Most Common Issue Among Females
- 29 females report Depression, the highest among all mental health issues.
- This suggests that female students may be more prone to long-term stress or emotional distress.

--

d.	Males Have Lower Mental Health Issue Reports Overall
- The number of males reporting Depression, Anxiety, and Panic Attacks is significantly lower than females.
- This could be due to underreporting, societal stigma, or genuine lower prevalence.

--

**RECOMMENDATIONS**
1.	Increase Mental Health Awareness & Support for Female Students
- Since females report higher cases of Depression, Anxiety, and Panic Attacks, universities should provide gender-sensitive mental health programs.
- Conduct regular mental health check-ins and offer targeted counseling sessions.

--

2.	Address Anxiety Among Male Students
- Even though the numbers are lower, Anxiety is still the most reported issue among males.
- Introduce stress management workshops, mindfulness sessions, and coping strategies to help students manage anxiety.

--

3.	Investigate Potential Underreporting Among Males
- The lower numbers for males could indicate that men are less likely to seek help due to stigma.
- Encourage mental health discussions tailored to male students to create a safe space for seeking support.

--

4.	Implement Mental Health Policies & Resources
- Provide easily accessible counseling services and mental health hotlines for students.
- Organize peer support groups where students can discuss their mental health challenges.

--

5.	Conduct Further Research on Underlying Causes
- The reasons behind the higher female prevalence in mental health issues should be explored.
- Consider factors like academic pressure, social expectations, or financial stress.

---

**C.	CGPA Relationship vs Mental Health**
1.	Higher CGPA is Associated with More Reported Mental Health Issues
- Students with higher CGPAs (3.00 - 4.00) report the most cases of depression, anxiety, and panic attacks. Example:
- 3.00 - 3.49 CGPA: 19 depression, 15 anxiety, 9 panic attacks.
- 3.50 - 4.00 CGPA: 12 depression, 18 anxiety, 18 panic attacks.
- This suggests that academic pressure may contribute to mental health challenges.

--

2.	Low CGPA Students Report Fewer Mental Health Issues
- Students in the 0 - 2.99 CGPA range have very few reported mental health issues. Example:
- 0 - 1.99 CGPA: 0 depression, 0 anxiety, 1 panic attack.
- 2.00 - 2.49 CGPA: 0 depression, 0 anxiety, 1 panic attack.
- 2.50 - 2.99 CGPA: 3 depression, 1 anxiety, 3 panic attacks.

**This could mean:**
- Lower-performing students may experience less academic pressure.
- They might be less likely to report mental health struggles due to other stressors (e.g., disengagement, lack of motivation, or external issues like finances).

--

3.	Anxiety is Highest in the Top CGPA Group
- The highest anxiety levels (18 cases) appear in the 3.50 - 4.00 CGPA group.
- This aligns with the idea that high-achieving students may experience more stress and pressure to maintain their grades.

--

4.	Panic Attacks Increase as CGPA Rises
- Students in the highest CGPA group (3.50 - 4.00) have the most panic attacks (18 cases).
- This may suggest that high expectations and academic demands trigger more intense stress reactions.

--

**RECOMMENDATIONS**
1.	Provide Stress Management Programs for High-Achieving Students
- Universities should implement stress-relief workshops, counseling, and mindfulness sessions for students aiming for top grades.
- Promote healthy study habits and work-life balance.

--

2.	Investigate Mental Health Among Low CGPA Students
- The low numbers of reported mental health issues in students with CGPA < 3.00 could mean underreporting or other hidden struggles.
- Conduct mental health awareness campaigns to encourage self-reporting and seeking help.

--

3.	Address Academic Pressure in Competitive Programs
- Departments with high CGPA expectations should introduce mental health support in their curriculum.
- Professors should encourage growth mindset strategies instead of grade-focused stress.

--

4.	Expand Access to University Counseling Services
- Ensure that counseling centers are accessible and de-stigmatized so that students feel comfortable seeking help.
- Offer anonymous surveys to assess actual stress levels beyond self-reported cases.

--

5.	Encourage Peer Support Groups: Create peer-led mental health support groups where students (especially those with high CGPA pressure) can discuss coping strategies and shared experiences.

---

**D.	Mental Health Across Year of Study**
1.	First-Year Students Have the Highest Mental Health Challenges
- 14 cases each for depression, anxiety, and panic attacks in Year 1.
- This suggests that transitioning into university life may be overwhelming.
--
Possible reasons:
- New academic environment & expectations
- Social adjustment & homesickness
- Financial or independent-related stress

--

2.	Mental Health Issues Decrease Slightly in Years 2 and 3
- Year 2: 10 depression, 10 anxiety, 8 panic attacks.
- Year 3: 10 depression, 8 anxiety, 10 panic attacks.
This indicate that students gradually adapt to academic and social life. However, panic attacks in Year 3 (10 cases) suggest that stress remains a concern.

--

3.	Final-Year Students Report the Least Mental Health Issues: Only 1-2 cases in Year 4 for all three conditions and this could mean:
- Adaptation & resilience – Final-year students may have developed better coping mechanisms.
- Survivor bias – Those who struggled with mental health earlier may have dropped out or stopped reporting.
- Avoidance or focus on graduation – Final-year students might suppress stress to focus on completing their studies.

---

**RECOMMENDATIONS**
1.	Strengthen First-Year Mental Health Support: Universities should increase orientation programs with a focus on mental well-being. They should also offer peer mentorship programs where seniors guide first-years through university life.

--

2.	Expand Academic & Psychological Support in Year 1 & 2
- Provide stress management workshops to help students adjust to academic demands.
- Train faculty & staff to identify students struggling with mental health early.

-- 

3.	Monitor & Support Year 3 Students for Panic Attacks: Since panic attacks remain high in Year 3, universities should introduce:
- Time management & exam stress workshops.
- Counseling sessions specifically for third-year students.

--

4.	Investigate Underreporting or Coping Mechanisms in Year 4: Since final year students report very few mental health issues, conduct surveys to see if they are:
- Hiding stress due to graduation pressure.
- Using different coping strategies (healthy or unhealthy).
- Simply more mentally resilient over time.

--

5.	Establish Year-Specific Mental Health Programs. For
- Year 1: Adjustment support, social integration, counseling.
- Year 2 & 3: Stress management, academic pressure workshops.
- Year 4: Career counseling, emotional preparation for life after graduation.

--- 

**E.	Mental Health Issues by Course Distribution**
1.	Engineering, BCS, and BIT have the highest mental health cases
- Engineering (26 students): Depression (9), Anxiety (8), Panic Attacks (8)
- BCS (18 students): Depression (5), Anxiety (6), Panic Attacks (5)
- BIT (10 students): Depression (5), Anxiety (8), Panic Attacks (4)
- These courses show a higher rate of mental health issues, possibly due to high academic pressure, demanding coursework, or competitive environments.

--

2.	Several Courses Have Zero or Very Few Mental Health Cases: Fields like Accounting, Banking Studies, Business Administration, Biotechnology, and Mathematics report zero cases of depression, anxiety, or panic attacks. This could be due to:
- Lower academic stress in these fields.
- Smaller sample sizes (if fewer students were surveyed from these fields).
- Students in these fields may be less likely to report mental health struggles.

--

3.	Humanities & Social Sciences Show Moderate Mental Health Issues
- Psychology (3 students): Depression (2), Anxiety (2), Panic Attacks (1)
- Laws (3 students): Depression (2), Anxiety (1), Panic Attacks (1)
- BENL (3 students): Depression (2), Anxiety (1), Panic Attacks (0)
- Communication (1 student): Depression (1), Anxiety (1), Panic Attacks (1)
- While not as high as Engineering or IT, stress in these fields could come from reading-intensive coursework, research workload, or career uncertainty.

--

4.	Some Unexpected Courses Report Mental Health Cases
- ALA (1 student): Depression (1), Panic Attack (1) – 100% rate
- ENM (1 student): Depression (1), Anxiety (1), Panic Attack (1) – 100% rate
- Marine Science (1 student): Depression (1), Anxiety (1), Panic Attack (1) – 100% rate
- These cases could indicate individual struggles rather than a widespread issue in these fields.

--

**RECOMMENDATIONS**
1.	Investigate Mental Health Support in High-Stress Fields
- Engineering, BCS, and BIT students may need additional academic and emotional support.
- Universities should introduce stress management programs, counseling services, and peer support groups in these departments.

--

2.	Analyze Causes of High Mental Health Issues in Certain Courses
- Are students in IT and Engineering struggling due to coursework difficulty, workload, or job market pressure?
- Are social science students (like Law, Psychology, and BENL) experiencing stress due to research, reading loads, or uncertainty about career prospects?
- Conduct in-depth interviews or focus groups with students to understand the root causes.

--

3.	Improve Awareness and Access to Mental Health Resources
- Many students may not seek help due to stigma.
- Universities should actively promote counseling services, stress workshops, and mental health hotlines.

--- 


**Statistical Analyses of Student Data**
---

In this section, we analyze key statistical measures for students' ages and CGPA midpoints using descriptive statistics. This helps to understand the distribution, central tendencies, and variability in the dataset.

Descriptive Analysis of Students’ Age
The analysis of students’ ages reveals an average (mean) age of 20.53 years, with a median age of 19 years. The mode, which represents the most frequently occurring age, is 18 years. This indicates that most students fall within the late teenage to early adulthood range.




The standard deviation (2.48) shows moderate variability in age, meaning that while most students are around 20 years old, there are some younger and older students in the dataset. The range (6 years) confirms this, as the youngest student is 18 years old while the oldest is 24 years old.

The standard error (0.247) is relatively low, suggesting that the sample mean is a good estimate of the actual population mean. Additionally, the dataset shows a slight positive skew (0.37), indicating that a few students are older than the average.


**Key Findings and Recommendations**
- The student population consists mainly of young adults, with a majority between 18 and 21 years old. Institutions can tailor student services, academic support, and mental health initiatives for this age group.
- The slight positive skew suggests that some students might be returning to school later or pursuing higher education at different ages. Universities should consider flexible learning programs for older students.

 ---
 
**Descriptive Analysis of CGPA Midpoints**

- The average CGPA midpoint is approximately 3.36, indicating that most students perform well academically, with CGPAs tending toward the higher range. The median CGPA midpoint (3.245) is slightly lower than the mean, suggesting a few students with very high CGPAs pull the average up. The mode (3.75) shows that the most common CGPA range is 3.50 – 4.00, meaning many students are high achievers.
- A negative skew (-2.72) confirms that most students have high CGPAs, while a smaller number struggle with lower CGPAs. Additionally, high kurtosis (8.60) indicates a peaked distribution, meaning many students cluster around high CGPAs, but a few outliers have very low CGPAs.
- The standard deviation (0.585) suggests moderate spread in CGPA values, while the range (2.755) highlights a notable difference between the lowest (0.995) and highest (3.75) CGPA midpoints.




Key Findings and Recommendations
•	Most students perform well academically, but a small group of students struggle with very low CGPAs. Targeted support (e.g., tutoring, mentorship, academic counseling) could help these students improve.
•	The negative skew suggests academic excellence is common, but it is crucial to ensure that high-performing students are not experiencing excessive academic pressure that may contribute to mental health issues.
•	Institutions should investigate the specific courses where students struggle to identify patterns that may indicate the need for curriculum adjustments or additional academic resources.


**Conclusion**
---

This report has provided an in-depth analysis of student mental health, demographics, and academic performance based on the dataset collected. Through data cleaning, visualization, and statistical analysis, we have uncovered key insights that highlight the prevalence of mental health issues among students, gender differences in mental health challenges, the relationship between CGPA and mental health, and variations in mental health concerns across different courses and years of study.

--
The findings indicate that mental health issues such as depression, anxiety, and panic attacks are present among students, with higher occurrences among female students. Additionally, while students with higher CGPAs tend to experience more mental health challenges, those with lower CGPAs remain a minority in the dataset. First-year students reported higher mental health issues compared to their senior counterparts, suggesting the need for better transition support programs. 

--
Furthermore, certain academic courses reported more mental health concerns than others, indicating the potential influence of workload, academic pressure, and field of study on students' well-being.

--
From a statistical perspective, the descriptive analysis of age and CGPA midpoints has provided valuable insights into the student population. Most students are young adults, and their academic performance leans towards the higher CGPA range, although some students struggle academically. These insights call for targeted interventions, including mental health awareness programs, academic counseling, and student support services to improve overall well-being and performance.


**Final Recommendations**
- Increase mental health support services through awareness programs, counseling, and therapy sessions.
- Enhance academic support for struggling students, including tutoring, mentorship, and study resources.
- Implement stress management programs to help students balance academic workload and personal well-being.
- Monitor high-risk student groups, such as first-year students and those in courses with high mental health concerns and provide targeted assistance.
- Encourage an open dialogue on mental health to reduce stigma and create a supportive academic environment.
--
By addressing these concerns, the institutions can create a more inclusive and supportive environment that fosters both academic excellence and student well-being.
