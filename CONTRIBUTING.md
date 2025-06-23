# Contributing to Single Cell Omics Knowledge Base

Thank you for your interest in contributing to our knowledge base! This guide will help you create high-quality, reproducible content that benefits the entire Single Cell Omics community.

## 🎯 Contribution Types

We welcome several types of contributions:

- **Analysis workflows**: Complete pipelines with code and interpretation
- **Protocols**: Step-by-step laboratory or computational procedures  
- **Tutorials**: Educational content for learning new methods
- **References**: Literature reviews and method comparisons
- **Bug fixes**: Corrections to existing content
- **Improvements**: Updates to documentation, code, or explanations

## 🚀 Quick Start Guide

### 1. Set Up Your Environment

```bash
# Fork and clone the repository
git clone https://github.com/YOUR-USERNAME/single-cell-omics-kb.git
cd single-cell-omics-kb

# Create a new branch
git checkout -b your-feature-branch

# Install required R packages
Rscript -e "
packages <- c('rmarkdown', 'knitr', 'here', 'sessioninfo')
install.packages(packages[!packages %in% installed.packages()])
"
```

### 2. Choose a Template

Navigate to the `templates/` folder and copy the appropriate template:

- `analysis_template.Rmd` - For analysis workflows
- `protocol_template.Rmd` - For protocols and procedures
- `tutorial_template.Rmd` - For educational content
- `reference_template.Rmd` - For reviews and comparisons

### 3. Create Your Content

```bash
# Copy a template to the appropriate folder
cp templates/analysis_template.Rmd analyses/your-analysis-name.Rmd

# Edit your content
# Use your preferred R/RStudio setup
```

## 📝 Content Guidelines

### R Markdown Best Practices

#### YAML Header
Always include a complete YAML header:

```yaml
---
title: "Your Descriptive Title"
author: "Your Name"
date: "`r Sys.Date()`"
output: 
  html_document:
    toc: true
    toc_float: true
    code_folding: show
    theme: flatly
    highlight: tango
bibliography: references.bib
---
```

#### Code Chunks
- Use descriptive chunk names: `{r load-libraries}`, `{r quality-control}`
- Set appropriate chunk options:
  ```r
  # For plots
  {r plot-umap, fig.width=8, fig.height=6, fig.cap="UMAP visualization"}
  
  # For long computations
  {r differential-expression, cache=TRUE, eval=TRUE}
  
  # For package loading (suppress messages)
  {r setup, include=FALSE}
  knitr::opts_chunk$set(echo = TRUE, warning = FALSE, message = FALSE)
  ```

#### Documentation Standards
- **Clear titles**: Use descriptive, searchable titles
- **Abstract/Summary**: Include a brief overview at the beginning
- **Prerequisites**: List required knowledge, software, or data
- **Step-by-step**: Break complex procedures into numbered steps
- **Interpretation**: Explain results and their biological significance
- **Session info**: Always include at the end

### Code Style

#### R Code
Follow the [tidyverse style guide](https://style.tidyverse.org/):

```r
# Good
library(Seurat)
library(dplyr)
library(ggplot2)

# Load data
seurat_obj <- readRDS("data/pbmc_3k.rds")

# Perform normalization
seurat_obj <- seurat_obj %>%
  NormalizeData() %>%
  FindVariableFeatures(selection.method = "vst", nfeatures = 2000)
```

#### File Organization
```r
# Always load libraries at the top
library(Seurat)
library(dplyr)

# Define functions early
calculate_metrics <- function(obj) {
  # Function code here
}

# Set parameters
n_features <- 2000
resolution <- 0.5
```

### Scientific Content

#### Reproducibility Requirements
- **Data availability**: Specify where data can be accessed
- **Software versions**: Include package versions and R version
- **Random seeds**: Set seeds for reproducible results
- **System requirements**: Note any special computational needs

#### Quality Standards
- **Biological context**: Explain the biological question being addressed
- **Method justification**: Explain why specific methods were chosen
- **Parameter selection**: Justify key parameter choices
- **Results interpretation**: Provide biological interpretation of findings
- **Limitations**: Acknowledge method limitations or caveats

## 📁 File Organization

### Naming Conventions
- Use lowercase with hyphens: `rna-seq-integration.Rmd`
- Be descriptive: `trajectory-analysis-monocle3.Rmd` not `analysis.Rmd`
- Include method/tool names when relevant

### Folder Structure
```
your-content.Rmd          # Main R Markdown file
your-content_files/       # Auto-generated folder for plots/cache
data/                     # Small example datasets (< 10MB)
scripts/                  # Additional R scripts if needed
```

### Large Files
- **Don't commit large files** (> 10MB) to the repository
- Use external hosting (Zenodo, FigShare) and provide download links
- Consider using `git-lfs` for moderately large files if necessary

## 🔄 Submission Process

### Before Submitting
1. **Test your code**: Ensure all chunks run without errors
2. **Knit successfully**: Verify the document knits to HTML
3. **Check links**: Ensure all external links work
4. **Proofread**: Check for typos and formatting issues
5. **Review guidelines**: Confirm compliance with all standards

### Pull Request Process
1. **Commit your changes**:
   ```bash
   git add .
   git commit -m "Add analysis: single-cell trajectory analysis with Monocle3"
   ```

2. **Push to your fork**:
   ```bash
   git push origin your-feature-branch
   ```

3. **Create pull request**:
   - Use a descriptive title
   - Fill out the pull request template
   - Link any relevant issues
   - Request review from maintainers

### Pull Request Template
When creating a PR, include:

```markdown
## Description
Brief description of your contribution

## Type of Content
- [ ] Analysis workflow
- [ ] Protocol/procedure
- [ ] Tutorial
- [ ] Reference/review
- [ ] Bug fix
- [ ] Documentation improvement

## Checklist
- [ ] Code runs without errors
- [ ] Document knits successfully
- [ ] Follows style guidelines
- [ ] Includes session information
- [ ] Added appropriate metadata
- [ ] Tested on sample data

## Additional Notes
Any special considerations or requirements
```

## 🏷️ Content Metadata

Include metadata in your YAML header:

```yaml
---
title: "Single-cell RNA-seq Analysis with Seurat"
author: "Jane Doe"
date: "`r Sys.Date()`"
output: 
  html_document:
    toc: true
    toc_float: true
categories: ["RNA-seq", "Seurat", "clustering"]
tags: ["single-cell", "transcriptomics", "R"]
level: "intermediate"  # beginner, intermediate, advanced
estimated_time: "2 hours"
prerequisites: ["Basic R knowledge", "Understanding of single-cell concepts"]
---
```

## 🤝 Review Process

### What We Look For
- **Scientific accuracy**: Correct methods and interpretations
- **Code quality**: Clean, well-documented, reproducible code
- **Clarity**: Clear explanations suitable for the target audience
- **Completeness**: All necessary information included
- **Formatting**: Consistent with style guidelines

### Review Timeline
- Initial review: 1-2 weeks
- Revision requests: Communicated via PR comments
- Final approval: After all requirements met

## 💡 Tips for Success

### Writing Tips
- **Start with an outline**: Plan your content structure
- **Use active voice**: Makes content more engaging
- **Include visuals**: Plots, diagrams, and screenshots help understanding
- **Provide context**: Explain why methods matter biologically

### Technical Tips
- **Version control**: Commit frequently with descriptive messages
- **Test environments**: Check that code works in clean R sessions
- **Document dependencies**: List all required packages and versions
- **Use relative paths**: Ensure portability across systems

### Community Engagement
- **Respond to feedback**: Address reviewer comments promptly
- **Ask questions**: Use GitHub Discussions if unsure about anything
- **Help others**: Review and comment on other contributions

## 🆘 Getting Help

- **GitHub Issues**: For bugs or feature requests
- **GitHub Discussions**: For questions about contributing
- **Maintainer contact**: Listed in README.md
- **Community Slack**: [Link if available]

## 📚 Resources

### Learning Resources
- [R Markdown Guide](https://rmarkdown.rstudio.com/lesson-1.html)
- [Git and GitHub Tutorial](https://happygitwithr.com/)
- [Tidyverse Style Guide](https://style.tidyverse.org/)

### Single-cell Resources
- [Current Best Practices in Single‐Cell RNA‐Seq Analysis](https://currentprotocols.onlinelibrary.wiley.com/doi/full/10.1002/cpmo.51)
- [Orchestrating Single-Cell Analysis with Bioconductor](https://osca.bioconductor.org/)

---

Thank you for contributing to the Single Cell Omics knowledge base! Your expertise helps advance the entire field. 🧬✨