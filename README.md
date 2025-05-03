# Student Performance Prediction

## Introduction

After spending several months exploring machine learning and statistical inference, I wanted to tackle a more meaningful and challenging problem beyond typical datasets like Iris or Titanic. My goal was to take on a real-world dataset that was completely new to me and apply my knowledge from scratch.

This project uses the [Student Performance Dataset](https://archive.ics.uci.edu/ml/datasets/Student+Performance), accompanied by the research paper:  
[Using Data Mining to Predict Secondary School Student Performance](http://www3.dsi.uminho.pt/pcortez/student.pdf).

## Objective

The objective of this project is to predict whether a student will fail a math course. I focused on predicting failures specifically, as identifying at-risk students early can enable timely interventions and more personalized academic support.

## Methodology

The target variable is `G3`, the final math grade. As outlined in the paper, this value is converted into a binary outcome:  
- **Pass:** G3 ≥ 10  
- **Fail:** G3 < 10

I applied the same binning approach to `G1` and `G2`, which represent prior grades.

### Key Features (in order of importance):
1. `G2` (second-period grade)  
2. `G1` (first-period grade)  
3. `School`  
4. `Absences`

When grade data is unavailable, `School` and `Absences` provide some predictive value. However, when `G1` and `G2` are known, they alone can drive model accuracy above 90%. For optimal results, I found that training the model with only two features at a time works best.

### Model

The final model is a **Linear Support Vector Machine (SVM)** with a regularization factor of 100. After testing other models including Naive Bayes, Logistic Regression, and Random Forest, the linear SVM provided the best and most consistent results.

## Results

Averaged over five trials, the model results are summarized below:

| Features Used        | G1 & G2 | G1 & School | School & Absences |
|----------------------|:-------:|:-----------:|:-----------------:|
| Paper Accuracy       | 0.919   | 0.838       | 0.706             |
| My Model Accuracy    | 0.9165  | 0.8285      | 0.6847            |
| False Pass Rate      | 0.096   | 0.12        | 0.544             |
| False Fail Rate      | 0.074   | 0.1481      | 0.2185            |

📌 [Why these metrics?](https://github.com/sachanganesh/student-performance-prediction/issues/1#issuecomment-508577754)

## Analysis

Without prior grade data, predicting student failure is quite difficult. Still, using just `School` and `Absences`, my model achieves ~68% accuracy. However, this comes with a high false pass rate—over 50%—meaning many failing students are misclassified as passing. This metric improves drastically as grade data (`G1`, `G2`) becomes available.

While the original authors switched between models (SVM and Naive Bayes) depending on the feature set, my approach uses a single linear SVM throughout. It achieves nearly the same performance with a simpler and more consistent setup. Additionally, while the original study relied on all available features (excluding grades) to reach 70.6% accuracy in one scenario, my model achieves comparable performance using only two features.

---

Created by [@kunalrathiaf](https://github.com/kunalrathiaf)  
Feel free to fork or contribute!
