# genetic-gene-selection
#  Genetic Gene Selection: Identifying Genes that Influence Phenotype

## 🧠 Objective

The primary goal of this project was to determine which genes among a set of 2000 significantly influence a given phenotype in laboratory mice.  
This involved analyzing high-dimensional genetic data where the number of predictors (genes) far exceeded the number of observations (samples), making it a perfect case for dimensionality reduction and regularized regression.

Understanding these gene–phenotype relationships provides critical insight into:
- **Genetic architecture** behind trait expression
- **Predictive modeling** using genomic data
- **Biomedical applications**, such as identifying targets for disease intervention

---

## 🧬 Dataset

- **Subjects**: 50 mice
- **Features**: Gene expression levels for 2000 genes (continuous predictors)
- **Target Variable**: A single quantitative phenotype per mouse

This setup resulted in a **p >> n** scenario — i.e., 2000 predictors but only 50 observations, posing statistical challenges for traditional regression techniques.

---

## 🛠️ Methodology

### 📉 Initial Data Diagnostics

- **Multicollinearity**: High multicolinearity present in the dataset
- **Linearity & Homoscedasticity**: Visual inspection of residuals and fitted plots suggested valid assumptions for regression analysis.

---

### 🔍 Feature Selection: Univariate Filtering

Due to high dimensionality, we first reduced the feature space using **correlation-based filtering**:

1. Calculated Pearson correlation between each gene and the phenotype.
2. Ranked genes by absolute correlation values.
3. Selected the **top 200 genes** for model training.

This ensured that only the most relevant variables were fed into our models.

---

### 🤖 Models Applied

We implemented and compared the following models on the reduced 200-variable dataset using an 80-20 train-test split:

| Model              | Description                                                                 |
|-------------------|------------------------------------------------------------------------------|
| Ridge Regression   | L2 regularization; shrinks coefficients but retains all predictors          |
| Lasso Regression   | L1 regularization; performs variable selection by zeroing out coefficients  |
| Elastic Net        | Combination of L1 and L2; balances sparsity and stability                   |
| Bayesian Ridge     | Bayesian version of Ridge; assumes normal priors for coefficients           |
| Bayesian Lasso     | Bayesian interpretation of Lasso; assumes Laplacian priors (sparse models)  |

---

### 📈 Model Performance Comparison

| Model              | R² Score  | MSE      | Std. Dev. of Residuals | Variance Score |
|-------------------|-----------|----------|-------------------------|----------------|
| Ridge Regression   | 0.9302    | 8646.03  | 90.30                   | 0.9342         |
| Lasso Regression   | 0.9576    | 5250.18  | 70.85                   | 0.9595         |
| Elastic Net        | 0.9576    | 5250.18  | 70.85                   | 0.9595         |
| Bayesian Ridge     | 0.9302    | 8645.96  | 90.30                   | 0.9342         |
| **Bayesian Lasso** | **0.9999**| **9.21** | **3.02**                | **0.9595**     |

> ✅ **Bayesian Lasso** significantly outperformed all others, offering excellent accuracy while also performing embedded feature selection through sparse coefficient estimation.

---

## 📌 Top 10 Genes Influencing the Phenotype

Using the absolute magnitude of coefficients from the Bayesian Lasso model, we identified the top 10 genes with the most influence on phenotype:

| Rank | Gene   | Coefficient |
|------|--------|-------------|
| 1    | X2     | 177.89      |
| 2    | X1     | 131.02      |
| 3    | X5     | 88.70       |
| 4    | X4     | 76.76       |
| 5    | X3     | 47.19       |
| 6    | X273   | 0.57        |
| 7    | X713   | 0.49        |
| 8    | X142   | 0.43        |
| 9    | X1628  | 0.35        |
| 10   | X472   | 0.34        |

These genes are strong candidates for further biological interpretation or validation.

---

## 🧪 Bayesian Perspective

Bayesian approaches assume **priors** over model parameters, leading to probabilistic coefficient estimates.

- **Ridge**: Assumes Gaussian priors → shrinks coefficients
- **Lasso**: Assumes Laplace (double exponential) priors → induces sparsity
- **Bayesian Lasso**: Captures uncertainty while promoting sparsity → ideal for genomic data

The **Bayesian Lasso** model’s predictive superiority and interpretability make it well-suited for high-dimensional biological datasets.

---

## 📘 Conclusion

- The Bayesian Lasso model achieved the **best performance** with nearly perfect R² and minimal prediction error.
- It successfully identified the most impactful genes influencing phenotype in a high-dimensional setup.
- This method bridges statistical rigor and biological relevance, providing a scalable approach to gene selection problems.

---


## 🚀 Future Work

- 📊 **Scale the study** to thousands of samples across different species or traits.
- 🧬 **Pathway analysis** of top genes to discover biological mechanisms.
- 🔬 **Wet lab validation** of selected genes in clinical or experimental settings.
- 🧠 **Apply deep learning models** (e.g., autoencoders, transformers) for non-linear patterns in gene data.

---


