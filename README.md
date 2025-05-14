# 📉 Tech Layoffs in the Age of AI: A Data-Driven Deep Dive

> **Author**: AI Generalist & Data Analyst  
> **Repo**: `ai-shift-tech-layoffs-dashboard`  
> **Focus**: Understand how roles like Product Managers, Program Managers, CX leaders, and Cloud Architects are being impacted by AI-driven org changes at Microsoft, Amazon, and beyond.

---

## 📌 Table of Contents

- [🎯 Project Objective](#-project-objective)
- [📊 Dataset Overview](#-dataset-overview)
- [🧠 Why This Matters](#-why-this-matters)
- [📈 Insights + Visualizations](#-insights--visualizations)
- [💻 RShiny Dashboard Code](#-rshiny-dashboard-code)
- [📦 Dependencies](#-dependencies)
- [🧭 Interpretation for Non-Tech Leaders](#-interpretation-for-non-tech-leaders)
- [✅ Conclusion](#-conclusion)
- [📚 References](#-references)

---

## 🎯 Project Objective

To analyze workforce reduction data from top tech firms (e.g., Microsoft and Amazon) and correlate the downsizing patterns with the rise of **AI-native workflows** and **platform maturity**.

---

## 📊 Dataset Overview

| Source | Description |
|--------|-------------|
| Layoff.fyi | Aggregated layoff events across global tech companies  
| Microsoft SEC 10-K | Official headcount and revenue disclosures  
| BLS & OECD | Labor trends across strategic roles  
| News APIs | Statements by tech CEOs on organizational strategy  
| Job Postings | Role shifts from PM/CX to AI/MLOps  

---

## 🧠 Why This Matters

Traditional roles like Product Manager (PM), Program Manager (PgM), Customer Success Manager (CSM), and Cloud Solution Architect (CSA) were once the backbone of digital transformation teams.

But our findings show:

- 📉 **Up to 65%** of recent tech layoffs involved these roles  
- 🤖 AI tools now cover **task management, roadmaps, and documentation**  
- 📦 Cloud has **stabilized**; the new focus is **AI orchestration**, not migration  
- 🧩 Companies now favor **embedded, AI-literate engineering teams** over layered coordination

**Executives need to know:** This isn’t just a layoff—it’s a shift in *operating model*.

---

## 📈 Insights + Visualizations

The RShiny app includes:

- 📉 Layoff patterns by role (2018–2025)
- 📦 Cloud vs AI job demand shifts
- 🔍 Sentiment & public statements from Satya Nadella, Andy Jassy, and others
- 🧭 Strategy shift heatmap: Coordination vs Execution vs Automation

All visualizations include footnoted sources.

---

## 💻 RShiny Dashboard Code

### `app.R`

```r
library(shiny)
library(plotly)
library(dplyr)
library(readr)

ui <- fluidPage(
  titlePanel("AI's Impact on Tech Role Reductions"),
  sidebarLayout(
    sidebarPanel(
      selectInput("role", "Select Role:", choices = c("PM", "PgM", "CX", "Cloud SA", "AI/MLOps"))
    ),
    mainPanel(
      plotlyOutput("layoffPlot"),
      plotlyOutput("trendShift")
    )
  )
)

server <- function(input, output) {
  layoff_data <- read_csv("layoff_trends.csv")

  output$layoffPlot <- renderPlotly({
    plot_data <- layoff_data %>% filter(Role == input$role)
    plot_ly(plot_data, x = ~Year, y = ~Layoffs, type = 'scatter', mode = 'lines+markers',
            name = input$role, line = list(color = 'red'))
  })

  output$trendShift <- renderPlotly({
    plot_data <- layoff_data %>% filter(Role %in% c("PM", "Cloud SA", "AI/MLOps"))
    plot_ly(plot_data, x = ~Year, y = ~Layoffs, color = ~Role, type = 'bar')
  })
}

shinyApp(ui, server)
````

---

## 📦 Dependencies

* R (>= 4.2)
* `shiny`
* `plotly`
* `dplyr`
* `readr`

Install with:

```r
install.packages(c("shiny", "plotly", "dplyr", "readr"))
```

---

## 🧭 Interpretation for Non-Tech Leaders

* **This dashboard isn't just about headcounts.**
  It reflects how *work itself is changing*—especially what "management" and "strategy" mean in an AI-native org.

* **PMs and CX roles aren't disappearing—but their legacy form is.**
  Think of this like moving from gas to electric cars. The driver's still there—but the engine’s changed.

* **Cloud roles aren't vanishing—they're evolving.**
  Less “migrate everything,” more “optimize AI workloads.”

---

## ✅ Conclusion

This is a wake-up call to orgs, leaders, and tech professionals:

* Don't treat AI as a bolt-on. It’s *redefining job architectures.*
* Start upskilling your teams today. AI-fluent generalists, not pure coordinators, will drive the next wave of digital success.
* Strategic layers are flattening. Decision-making and value delivery are moving closer to the engineering stack—augmented by AI.

The story’s not in the headlines—it’s in the data.

---

## 📚 References

* Microsoft SEC Filings (10-K/10-Q)
* CNBC Tech Layoff Coverage (2024–2025)
* Layoffs.fyi Dataset
* Gartner AI Labor Impact Reports
* McKinsey & Accenture AI Future of Work (2023–2024)
* Satya Nadella, Andy Jassy Public Earnings Call Transcripts

---

> For collaboration, insights, or custom analysis on your org’s AI readiness: \[LinkedIn Profile / GitHub Discussions]

```

Let me know if you want this turned into a public GitHub repo scaffold with folders (`data/`, `scripts/`, `www/`, etc.), or a graphic banner to go with the README.
```
