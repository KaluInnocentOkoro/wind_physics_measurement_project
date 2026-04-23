# Exercise 1: Handling and Preprocessing of Measurement Data
[cite_start]**Wind Physics Measurement Project, Summer Term 2026** [cite: 3]  
[cite_start]**Matthias Wächter, February 25, 2026** [cite: 4]

---

## 1. Introduction
[cite_start]The aim of this exercise is to handle raw measurement data to perform quantitative analyses[cite: 6]. [cite_start]This is often the most time-consuming step in data analysis[cite: 7]. [cite_start]The exercise uses **1 Hz measurement data** from the German **FINO I platform**[cite: 8].

### Report and Evaluation
* [cite_start]**Requirement:** Submit one short report per group[cite: 14].
* [cite_start]**Content:** Include method explanations, figures, and discussions[cite: 14].
* [cite_start]**Minimum Work:** Write at least one sentence for each numbered task[cite: 15].
* [cite_start]**Code:** You must submit your **Matlab code** along with the report[cite: 17].
* [cite_start]**Submission Format:** Submit a single file (e.g., a zip archive) with a clear group name[cite: 20].

---

## 2. Software
* [cite_start]**Matlab:** The primary tool for the course; university license pools are available[cite: 25, 27].
* [cite_start]**GNU Octave:** A free alternative (version $\ge4.0.0$ required)[cite: 29, 30].
* [cite_start]**Support:** Teaching support is only provided for Matlab and Octave[cite: 33].

---

## 3. Preparation
1. [cite_start]**Data:** Download `1301.txt.zip` from Stud-IP[cite: 36].
2. [cite_start]**Table Format:** The ASCII table contains[cite: 39]:
    * **Time**: Timestamp.
    * **uXX**: Cup anemometer wind speed at height XX m.
    * **dXX**: Wind vane direction at height XX m.

---

## 4. Tasks

### Task 1: Importing the Data
* [cite_start]Load data into the workspace and save it as a **.mat** file for efficiency[cite: 42].
* [cite_start]**Cleaning:** Replace all **"-999"** values (invalid data) with **NaN**[cite: 43, 44].
* [cite_start]**Hint:** Use `readtable()` in Matlab for the fastest import[cite: 46].

### Task 2: Continuous Time Axis
* [cite_start]Fill time gaps so the data has a constant **1 s sampling lag** for the entire month[cite: 55, 56].
* [cite_start]**Hint:** Use `datenum()` to convert timestamps to seconds since the start of measurements[cite: 59, 60].

### Task 3: 10-Minute Averaging
* [cite_start]Compute non-overlapping **10-minute mean values** and **standard deviations**[cite: 64, 65].
* [cite_start]**Condition:** Only compute values for intervals with at least **50% valid measurements**[cite: 67].
* [cite_start]**Plotting:** Plot 10-minute means of **u90** for **2013-01-30** including $(\overline{u} \pm \sigma_u)$[cite: 69, 70].
* [cite_start]**Discussion:** Discuss whether the mean value and standard deviation are stationary during this day[cite: 72].

### Task 4: Extreme Values (Spikes)
* [cite_start]Identify "spikes" using the **$5\sigma$ criterion** (values deviating more than 5 standard deviations from the mean)[cite: 75, 77].
* [cite_start]Find and plot a 10-minute interval from the **100 m anemometer** containing such an event[cite: 78].
* [cite_start]**Discussion:** Determine if your example is a real measurement or an error[cite: 80].

### Task 5: Increment PDF
* [cite_start]Compute the Probability Density Function (PDF) of wind speed increments $\delta u_{\tau} = u(t+\tau) - u(t)$ for **$\tau = 1s$**[cite: 138].
* [cite_start]Normalize data to **unit standard deviation** and plot in a **semi-logarithmic scale**[cite: 140, 141].
* [cite_start]**Comparison:** Add a Gaussian PDF of unit standard deviation to the plot[cite: 142].

### Task 6: Tower Shadow
* [cite_start]Compute the difference between the **100 m and 90 m anemometers** and plot against wind direction[cite: 169].
* [cite_start]Identify angles where deviations occur due to **lightning protection spikes** and the **tower shadow**[cite: 171].

---

## 5. Legal Note
* [cite_start]**Data Usage:** FINO data is free for scientific use within the EU[cite: 177].
* [cite_start]**Cleanup:** You must delete all data once the Laboratory Project is passed[cite: 178].
