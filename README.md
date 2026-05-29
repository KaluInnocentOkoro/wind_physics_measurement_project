# Exercise 1: Handling and Preprocessing of Measurement Data

**Course:** Wind Physics Measurement Project  
**Term:** Summer Term 2026  
**Instructor:** Matthias Wächter  
**Date:** February 25, 2026  

---

## 1. Introduction

The aim of this exercise is to handle raw measurement data so that quantitative analyses can be performed. This is often one of the most time-consuming steps in measurement data analysis.

The exercise uses **1 Hz measurement data** from the German **FINO I platform**. The data will be processed and analyzed to produce meaningful statistical results, plots, and discussions.

---

## 2. Report and Evaluation

Each group is expected to submit one short report for the entire exercise.

The report should include:

- Explanation of the methods used
- Figures showing the results
- Discussion of the findings
- Documentation of the data processing steps
- MATLAB code used for the analysis

For each numbered task, at least one sentence should be written.

### Submission Format

Submit only one file per group, preferably as a `.zip` archive.

Example filename:

```text
Report_Topic_1_Group_3.zip
```

---

## 3. Software

The recommended software for this exercise is **MATLAB**.

### Supported Tools

- **MATLAB**: Main software for the course
- **GNU Octave**: Free alternative to MATLAB

For GNU Octave, use version:

```text
>= 4.0.0
```

For most tasks in Octave, the statistics package may need to be loaded.

Teaching support is provided mainly for MATLAB and Octave. Other software may be used, but support is not guaranteed.

---

## 4. Preparation

### 4.1 Download the Data

Download the file:

```text
1301.txt.zip
```

from:

```text
Stud-IP → WPMP → Files → General Folder → Topic 1: Data Handling
```

### 4.2 Data File Description

After uncompressing the file, the data are stored in an ASCII table.

The table contains the following columns:

```text
Time
d90
d33
u100
u90
u80
u70
u60
u50
u40
u33
```

### 4.3 Meaning of Columns

| Column | Description |
|---|---|
| `Time` | Timestamp |
| `uXX` | Cup anemometer wind speed at height `XX` m |
| `dXX` | Wind vane direction at height `XX` m |

Examples:

| Column | Meaning |
|---|---|
| `u100` | Wind speed at 100 m |
| `u90` | Wind speed at 90 m |
| `d90` | Wind direction at 90 m |
| `d33` | Wind direction at 33 m |

---

# 5. Tasks

---

## Task 1: Importing the Data

Load the data into the MATLAB or Octave workspace.

Save the imported data as a MATLAB binary file:

```text
.mat
```

This allows efficient reading during later processing steps.

### Data Cleaning

Invalid data values are written as:

```text
-999
```

Replace all occurrences of `-999` with:

```matlab
NaN
```

This allows MATLAB to handle invalid or missing data efficiently.

Also report how many `-999` values were found.

### MATLAB Hint

Use:

```matlab
readtable()
```

This is recommended for fast data import.

---

## Task 2: Generating a Continuous Time Axis

The timestamps do not always follow a continuous 1-second sampling interval. Some larger time gaps may exist.

Fill the gaps so that the complete dataset has a constant sampling interval of:

```text
1 s
```

for the entire month.

This is especially useful for calculations involving fixed time lags, such as the wind speed increment analysis.

### Suggested Method

1. Convert all timestamps to seconds since the beginning of the measurement.
2. Create a continuous time vector with 1-second spacing.
3. Create a new data table or matrix with this continuous time axis.
4. Fill missing measurement values with `NaN`.
5. Insert the available measurement data at the correct time positions.

### MATLAB Hint

Use:

```matlab
datenum()
```

to help convert timestamps into numerical time values.

---

## Task 3: Averaging to 10-Minute Mean Values

Compute non-overlapping **10-minute mean values** for all data channels.

Also compute the corresponding **standard deviations** for each 10-minute interval.

The processed data should be stored again in MATLAB binary format:

```text
.mat
```

### Important Conditions

For each 10-minute interval:

- Use non-overlapping intervals.
- Include standard deviations.
- Treat wind direction as circular data.
- Only compute statistics if at least **50% of the measurements are valid**.

Since each 10-minute interval contains:

```text
10 min × 60 s = 600 samples
```

at least:

```text
300 valid samples
```

are required.

### Required Wind Speed Plot

Plot the 10-minute mean values of:

```text
u90
```

for the day:

```text
2013-01-30
```

The plot should include:

- Mean wind speed: `u`
- Mean plus standard deviation: `u + σu`
- Mean minus standard deviation: `u - σu`

### Required Wind Direction Plot

Create a similar plot for wind direction on the same day.

For the wind direction plot, standard deviations are not required.

### Discussion

Discuss the statistical properties of the wind speed plot.

Consider the following questions:

- Is the mean wind speed stationary during the day?
- Is the standard deviation stationary during the day?
- What changes or patterns can be observed?
- What might explain these changes?

---

## Task 4: Extreme Values

Sometimes, extremely high or low values are recorded by the measurement system. These values are called **spikes**.

The task is to determine whether these spikes represent real extreme wind events or erroneous measurements.

### 5σ Criterion

A common procedure is to treat values as suspicious if they deviate from the 10-minute mean by more than five standard deviations.

Mathematically:

```math
|u(t) - \bar{u}| > 5\sigma
```

where:

- `u(t)` is the instantaneous wind speed
- `\bar{u}` is the 10-minute mean wind speed
- `σ` is the standard deviation of the 10-minute interval

### Required Analysis

Find a 10-minute interval from the:

```text
100 m anemometer
```

that contains an event exceeding the `5σ` threshold.

Plot this interval and include horizontal lines for:

- Mean wind speed
- Mean plus and minus one standard deviation
- Mean plus and minus five standard deviations

### Discussion

Discuss whether the selected event is likely to be:

- A real wind event, or
- A measurement error

Consider the following questions:

- What assumptions are implied by the `5σ` criterion?
- Are these assumptions valid for wind measurements?
- Does the spike also appear in nearby anemometers?
- Is the spike physically realistic?
- How long does the spike last?
- Could it be caused by sensor or logging errors?

---

## Task 5: Increment PDF

Compute the probability density function, PDF, of the wind speed increments at 90 m.

The wind speed increment is defined as:

```math
\delta u_{\tau} = u(t + \tau) - u(t)
```

Use a time lag of:

```math
\tau = 1 \text{ s}
```

Use the complete month of data to obtain a well-defined PDF.

### Normalization

Normalize the wind speed increments to unit standard deviation:

```math
\frac{\delta u_{\tau}}{\sigma(\delta u_{\tau})}
```

### Required Plot

Plot the PDF using a semi-logarithmic scale.

Also add a Gaussian PDF with unit standard deviation to the same plot.

### MATLAB Hints

Use:

```matlab
histcounts()
```

to compute the histogram-based PDF.

Use:

```matlab
normpdf()
```

to generate the Gaussian PDF.

Use:

```matlab
semilogy()
```

to plot the PDF on a semi-logarithmic scale.

### Discussion

Discuss the shape of the measured increment PDF.

Consider the following questions:

- What do you observe for small values of `δu`?
- What do you observe for extreme values of `δu`?
- Are extreme wind speed changes more likely than predicted by a Gaussian PDF?
- How does the measured PDF compare with the Gaussian curve?
- What does the logarithmic scale reveal about rare events?

---

## Task 6: Tower Shadow

Every meteorological tower affects wind measurements because the tower structure disturbs the wind flow.

For the FINO I tower, this effect is especially important because of the strong offshore tower structure.

### Required Analysis

Using the stored 10-minute wind speed averages, compute the difference between the 100 m and 90 m anemometers:

```math
\Delta u = \bar{u}_{100} - \bar{u}_{90}
```

Plot this wind speed difference against wind direction.

### Required Plot

The plot should have:

```text
x-axis: Wind direction [°]
y-axis: Wind speed difference [m/s]
```

Bin-averaged values and error bars are not required.

### Discussion

Identify the wind direction angles where deviations occur due to:

- Lightning protection spikes
- Tower shadow

Describe the nature of these deviations.

Consider:

- At which wind directions are the deviations strongest?
- Are the deviations positive or negative?
- What do they suggest about flow disturbance around the mast?
- How do they relate to the physical tower structure?

---

# 6. Presentation Topics

## Presentation Topic A

Explain your solution and results for:

1. Task 1: Importing the data
2. Task 2: Generating a continuous time axis
3. Task 3: Averaging to 10-minute mean values
4. Task 4: Extreme values
5. Task 5: Increment PDF

---

## Presentation Topic B

Explain your solution and results for:

1. Task 1: Importing the data
2. Task 2: Generating a continuous time axis
3. Task 3: Averaging to 10-minute mean values
4. Task 4: Extreme values
5. Task 6: Tower shadow analysis

---

# 7. FINO I Data Legal Note

The FINO data were provided by the **Federal Maritime and Hydrographic Agency**, also known as **BSH**.

The data are free of charge for scientific use within the European Union.

After successfully passing the Laboratory Project, all downloaded FINO data should be deleted.

For further research use, an account should be requested through the BSH webpage.

---

# 8. Suggested Folder Structure

```text
exercise-1-data-handling/
│
├── README.md
├── data/
│   └── 1301.txt
│
├── scripts/
│   ├── task1_import_data.m
│   ├── task2_continuous_time_axis.m
│   ├── task3_10min_averaging.m
│   ├── task4_extreme_values.m
│   ├── task5_increment_pdf.m
│   └── task6_tower_shadow.m
│
├── processed_data/
│   └── results.mat
│
├── figures/
│   ├── task3_u90_10min_mean.png
│   ├── task3_wind_direction.png
│   ├── task4_extreme_event.png
│   ├── task5_increment_pdf.png
│   └── task6_tower_shadow.png
│
└── report/
    └── Report_Topic_1_Group_X.pdf
```

---

# 9. Submission Checklist

Before submitting, make sure the final archive contains:

- [ ] Final report
- [ ] MATLAB or Octave scripts
- [ ] Generated figures
- [ ] Processed `.mat` files, if required
- [ ] Clear filename with group number

Recommended final archive name:

```text
Report_Topic_1_Group_X.zip
```
