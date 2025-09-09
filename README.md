# HL_BM_analysis
Analysis of BM from HL patients.
# Required packages
library(survival)
library(survminer)

# -------------------------------------------------------------------
# Load dataset
# Replace "example_dataset.csv" with your actual dataset name/path.
# In the repository, provide only a mock or simulated dataset.
# -------------------------------------------------------------------
data <- read.csv("data/example_dataset.csv")

# Create survival object
surv_obj <- Surv(time = data$Time_Relapse,
                 event = data$Relapse_Y_N_cod)

# Kaplan-Meier model (overall survival)
km_fit <- survfit(surv_obj ~ 1, data = data)

# Kaplan-Meier by groups (example with categorical variable)
km_fit <- survfit(Surv(Time_Relapse, Relapse_Y_N_cod) ~ Biomarker_group,
                  data = data)

# Basic survival plot
ggsurvplot(km_fit,
           data = data,
           pval = TRUE,
           conf.int = TRUE,
           risk.table = TRUE,
           ggtheme = theme_minimal(),
           legend.labs = c("Biomarker Low", "Biomarker High"),
           xlab = "Time (months)",
           ylab = "Survival probability")

# Example of a customized survival plot
plot_km <- ggsurvplot(
  km_fit,
  data = data,
  pval = TRUE,
  conf.int = TRUE,
  risk.table = TRUE,
  ggtheme = theme_minimal(),
  legend.labs = c("Red Marrow Low, T0", "Red Marrow High, T0"),
  legend = "top",
  palette = c("#b00f1b", "#f6959c")
)
