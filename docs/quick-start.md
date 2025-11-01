# Quick Start Guide

Get started with the Synthea Pilot Study Methodology in minutes with this comprehensive quick start guide.

## 🚀 Quick Setup

### 1. Clone and Install

```bash
# Clone the repository
git clone https://github.com/ahidayatxx/Synthea-Pilot-Study-Methodology-.git
cd Synthea-Pilot-Study-Methodology

# Create virtual environment
python -m venv synthea-methodology-env
source synthea-methodology-env/bin/activate  # Windows: synthea-methodology-env\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Download Synthea

```bash
# Download Synthea (if not already available)
wget https://github.com/synthetichealth/synthea/releases/download/v3.2.0/synthea-with-dependencies.jar

# Or use curl
curl -L -o synthea-with-dependencies.jar https://github.com/synthetichealth/synthea/releases/download/v3.2.0/synthea-with-dependencies.jar
```

### 3. Generate Your First Synthetic Dataset

```bash
# Run basic hypertension cohort generation
java -jar synthea-with-dependencies.jar \
  -c config/hypertension_example.properties \
  -p 1000 \
  -s 2020-01-01 \
  -e 2023-12-31
```

## 📊 Run Your First Analysis

### Basic Analysis Example

```python
# Create analysis script
from methodology import SyntheaAnalyzer

# Initialize analyzer
analyzer = SyntheaAnalyzer(data_path="./output/hypertension_pilot_study/csv")

# Run basic analysis
results = analyzer.run_basic_analysis()

print("Analysis Results:")
print(f"- Total Patients: {results['total_patients']}")
print(f"- Total Encounters: {results['total_encounters']}")
print(f"- Average BP: {results['avg_bp']}")
```

### Advanced Analysis Example

```python
# Run comprehensive analysis
advanced_results = analyzer.run_comprehensive_analysis()

# Sequence Analysis
print("Sequence Analysis:")
for pattern, frequency in advanced_results['sequence_patterns'].items():
    print(f"  {pattern}: {frequency}%")

# Network Analysis
print("Network Analysis:")
print(f"  Network Density: {advanced_results['network']['density']}")
print(f"  Communities: {advanced_results['network']['communities']}")

# Mixed-Methods Integration
print("Mixed-Methods Insights:")
for insight in advanced_results['mixed_methods']['key_insights']:
    print(f"  - {insight}")
```

## 🎯 Example Case Study

### Hypertension Telemedicine Management

Follow the complete example in `examples/hypertension-telemedicine/`:

```bash
# Navigate to example
cd examples/hypertension-telemedicine

# Run the complete analysis pipeline
python run_complete_analysis.py

# View results
open results/analysis_report.html
```

### Key Features Demonstrated

1. **Sequence Analysis**: Patient behavior pattern identification
2. **Time Series Analysis**: Temporal trend detection
3. **Network Analysis**: Care relationship mapping
4. **Mixed-Methods Integration**: Qualitative-quantitative synthesis

## 📁 Essential Files

### Configuration Files

#### Synthea Configuration (`config/hypertension_example.properties`)
```properties
# Basic configuration
generate.patients.population = 1000
generate.start.date = 2020-01-01
generate.end.date = 2023-12-31

# Hypertension specific
generate.hypertension.prevalence = 0.35
generate.primary.conditions = hypertension

# Export settings
exporter.csv.folder = ./output/hypertension_pilot_study/csv
exporter.csv.format = true
```

#### Analysis Configuration (`config/analysis_config.yaml`)
```yaml
analysis:
  sequence_analysis:
    enabled: true
    min_sequence_length: 3
    max_patterns: 50

  time_series:
    enabled: true
    frequency: "monthly"
    method: "decomposition"

  network_analysis:
    enabled: true
    include_patient_patient: true
    community_detection: true

  mixed_methods:
    enabled: true
    synthetic_qualitative: true
    integration_method: "convergent"
```

### Key Scripts

#### Data Generation (`scripts/generate_data.py`)
```python
#!/usr/bin/env python3
"""Synthetic data generation script"""

import subprocess
import yaml

def generate_cohort(config_path):
    """Generate synthetic patient cohort"""

    # Load configuration
    with open(config_path, 'r') as f:
        config = yaml.safe_load(f)

    # Build Synthea command
    cmd = [
        "java", "-jar", "synthea-with-dependencies.jar",
        "-c", config_path,
        "-p", str(config['population_size']),
        "-s", config['start_date'],
        "-e", config['end_date']
    ]

    # Execute generation
    result = subprocess.run(cmd, capture_output=True, text=True)

    if result.returncode == 0:
        print("✅ Synthetic data generated successfully")
        return True
    else:
        print(f"❌ Generation failed: {result.stderr}")
        return False

if __name__ == "__main__":
    generate_cohort("config/hypertension_example.properties")
```

## 🔧 Customization Guide

### Create Your Own Study

#### 1. Define Your Research Question
```python
research_question = {
    "population": "Your target population",
    "intervention": "Your intervention of interest",
    "outcomes": "Your primary and secondary outcomes",
    "context": "Your healthcare context"
}
```

#### 2. Configure Synthea
```properties
# Custom configuration
generate.patients.population = 2000
generate.your_condition.prevalence = 0.25
generate.your_intervention.encounters = true
```

#### 3. Customize Analysis
```python
# Custom analysis pipeline
class CustomAnalyzer(SyntheaAnalyzer):
    def custom_analysis(self):
        """Your custom analysis method"""
        # Implementation here
        pass

    def custom_visualization(self):
        """Your custom visualization method"""
        # Implementation here
        pass
```

## 📊 Understanding Results

### Output Structure

```
results/
├── data_summary.csv          # Basic data statistics
├── sequence_patterns.json    # Behavioral pattern analysis
├── network_analysis.html     # Interactive network visualization
├── time_series_plots/        # Temporal trend visualizations
├── mixed_methods_report.md   # Integrated findings report
└── analysis_summary.html     # Complete analysis dashboard
```

### Key Metrics

#### Population Characteristics
- **Cohort Size**: Total number of synthetic patients
- **Demographics**: Age, gender, ethnicity distributions
- **Clinical Characteristics**: Disease prevalence and severity

#### Engagement Metrics
- **Visit Frequency**: Average encounters per patient
- **Medication Adherence**: Prescription fill patterns
- **Monitoring Frequency**: Vital sign measurement patterns

#### Network Metrics
- **Network Density**: Overall connectivity in care networks
- **Centrality Measures**: Key providers and patients
- **Community Structure**: Natural groupings and clusters

## 🛠️ Troubleshooting

### Common Issues

#### Synthea Generation Fails
```bash
# Check Java version
java -version

# Ensure sufficient memory
java -Xmx4g -jar synthea-with-dependencies.jar ...

# Check configuration file syntax
java -jar synthea-with-dependencies.jar --help
```

#### Analysis Errors
```python
# Check data availability
import os
assert os.path.exists("output/hypertension_pilot_study/csv"), "Data not found"

# Verify data format
import pandas as pd
patients = pd.read_csv("output/hypertension_pilot_study/csv/patients.csv")
print(patients.head())
```

#### Memory Issues
```python
# Process data in chunks
chunk_size = 1000
for chunk in pd.read_csv('large_file.csv', chunksize=chunk_size):
    process_chunk(chunk)
```

### Performance Optimization

#### Large Datasets
```python
# Use efficient data types
dtypes = {
    'PATIENT': 'category',
    'DATE': 'datetime64[ns]',
    'SYSTOLIC_BP': 'float32'
}
data = pd.read_csv('file.csv', dtype=dtypes)
```

#### Network Analysis
```python
# Limit network size for large cohorts
max_nodes = 1000
if len(network.nodes()) > max_nodes:
    network = network.subgraph(list(network.nodes())[:max_nodes])
```

## 📚 Next Steps

### Learning Resources

1. **Documentation**: Read comprehensive methodology docs
2. **Examples**: Study additional case studies
3. **Tutorials**: Complete step-by-step tutorials
4. **API Reference**: Detailed function documentation

### Community

1. **GitHub Issues**: Ask questions and report problems
2. **Discussions**: Join community conversations
3. **Contributions**: Contribute improvements and examples
4. **Collaboration**: Find research collaborators

### Advanced Topics

1. **Custom Analysis**: Develop domain-specific analyses
2. **Integration Methods**: Explore advanced mixed-methods approaches
3. **Visualization**: Create custom visualizations
4. **Publication**: Prepare academic papers and presentations

## 🎉 Success!

You've successfully set up the Synthea Pilot Study Methodology and generated your first synthetic cohort analysis!

### What's Next?

- **Explore Examples**: Check out additional case studies
- **Customize**: Adapt the framework to your research needs
- **Contribute**: Share your improvements with the community
- **Publish**: Use the methodology in your research

### Need Help?

- **Documentation**: Check comprehensive docs
- **Issues**: Report problems on GitHub
- **Community**: Join discussions
- **Email**: Contact maintainers directly

---

Happy researching! 🚀