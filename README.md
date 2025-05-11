# evaluation-metrics-in-hallucination
# RGB Hallucination Evaluator

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Google Gemini](https://img.shields.io/badge/LLM-Gemini%202.0-green)](https://ai.google.dev/)

A robust framework for evaluating hallucinations in Large Language Model outputs using the RGB framework powered by Google's Gemini 2.0.

## 🔍 Overview

The RGB Hallucination Evaluator provides a comprehensive approach to identify and measure three critical dimensions of hallucinations in LLM-generated content:

- **R**etrieval Hallucination: Factual errors or made-up information
- **G**eneration Hallucination: Internal inconsistencies or logical errors
- **B**ias Hallucination: Unfounded assumptions or biased framing

This tool is essential for researchers, developers, and organizations working with LLMs who need to ensure the reliability and factual accuracy of AI-generated content.

## ✨ Features

- 📊 Comprehensive scoring across three hallucination dimensions
- 📝 Detailed analysis with specific examples of problematic statements
- 🔄 Supports evaluation with or without reference text
- 🧠 Powered by Google's Gemini 2.0 LLM
- 📈 Provides an overall hallucination score with human-readable interpretation
- 🔍 Identifies bias indicators through specialized word lists
- 🛠️ Simple Python API for easy integration

## 📋 Requirements

- Python 3.8+
- Google Generative AI Python SDK
- NLTK
- NumPy

## 🚀 Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/rgb-hallucination-evaluator.git
cd rgb-hallucination-evaluator

# Install dependencies
pip install -r requirements.txt

# Set up your Gemini API key
export GEMINI_API_KEY="your_api_key_here"
```

## 📘 Usage

### Basic Example

```python
from rgb_hallucination_evaluator import RGBHallucinationEvaluator

# Initialize the evaluator
evaluator = RGBHallucinationEvaluator()

# Evaluate a response
results = evaluator.evaluate(
    response_text="The Great Pyramid of Giza was built in 2560 BCE and stands 481 feet tall.",
    reference_text="The Great Pyramid of Giza was built in approximately 2560 BCE during the Fourth Dynasty of Egypt's Old Kingdom. It stands 138 meters (approximately 455 feet) tall.",
    query_text="Tell me about the Great Pyramid of Giza."
)

# Print the overall hallucination score
print(f"Overall hallucination score: {results['overall_hallucination_score']:.2f}/1.00")
print(f"Interpretation: {results['interpretation']}")
```

### Full Evaluation Report

The evaluator returns a detailed dictionary with the following structure:

```python
{
    "overall_hallucination_score": 0.42,  # Combined weighted score
    "retrieval_hallucination": {
        "score": 0.65,  # Factual accuracy score
        "hallucinated_statements": [
            {
                "statement": "The pyramid stands 481 feet tall.",
                "explanation": "The actual height is approximately 455 feet."
            }
        ],
        "reasoning": "The response contains specific factual errors..."
    },
    "generation_hallucination": {
        "score": 0.2,  # Logical consistency score
        "inconsistencies": [...],
        "reasoning": "..."
    },
    "bias_hallucination": {
        "score": 0.3,  # Bias and assumption score
        "biased_elements": [...],
        "reasoning": "...",
        "bias_indicators_found": ["always", "clearly"],
        "bias_indicator_count": 2
    },
    "interpretation": "Fair: Response contains moderate hallucinations that somewhat impact quality"
}
```

### Command-line Usage

```bash
python -m rgb_hallucination_evaluator --response "Your response text" --reference "Your reference text" --query "Your query"
```

## 🔧 Configuration

The evaluator can be customized in several ways:

```python
# Custom API key
evaluator = RGBHallucinationEvaluator(api_key="your_api_key_here")

# Evaluate without reference text (common knowledge mode)
results = evaluator.evaluate(response_text="Your text here")

# Evaluate with reference but no query
results = evaluator.evaluate(
    response_text="Your response text",
    reference_text="Your reference text"
)
```

## 📊 Score Interpretation

| Score Range | Interpretation |
|-------------|----------------|
| 0.0 - 0.1   | Excellent: Response contains virtually no hallucinations |
| 0.1 - 0.3   | Good: Response contains minor hallucinations that don't significantly impact quality |
| 0.3 - 0.5   | Fair: Response contains moderate hallucinations that somewhat impact quality |
| 0.5 - 0.7   | Poor: Response contains substantial hallucinations that significantly impact quality |
| 0.7 - 1.0   | Very Poor: Response is dominated by hallucinations, making it unreliable |

## 🧪 Example

```python
response_text = """
The Great Pyramid of Giza was built in 2560 BCE and stands 481 feet tall. It was constructed by Emperor Napoleon
during his Egyptian campaign to commemorate his victories. The pyramid contains exactly 2,300,000 limestone blocks,
each weighing precisely 2.5 tons. Scientists recently discovered a hidden chamber containing ancient alien technology
that powered the entire Egyptian civilization.
"""

reference_text = """
The Great Pyramid of Giza was built in approximately 2560 BCE during the Fourth Dynasty of Egypt's Old Kingdom.
It stands 138 meters (approximately 455 feet) tall and was the tallest man-made structure in the world for more than
3,800 years. It was built as a tomb for the Pharaoh Khufu (Cheops). The pyramid is estimated to contain between
2.3 million and 2.6 million stone blocks, with an average weight ranging from 2.5 to 15 tons.
"""

query_text = "Tell me about the Great Pyramid of Giza."

results = evaluator.evaluate(
    response_text=response_text,
    reference_text=reference_text,
    query_text=query_text
)

print(json.dumps(results, indent=2))
```

## 📖 How It Works

The RGB Hallucination Evaluator uses a three-dimensional approach to evaluate hallucinations:

1. **Retrieval Hallucination**: Compares the response against reference text or common knowledge to identify factual errors or fabricated information.

2. **Generation Hallucination**: Analyzes the internal consistency and logical coherence of the response, regardless of factual accuracy.

3. **Bias Hallucination**: Detects unfounded assumptions, unjustified assertions, and biased framing through both pattern matching and LLM-based analysis.

The final score is a weighted combination of these three dimensions, with retrieval and generation typically given higher weight than bias.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- Google Gemini for providing the powerful evaluation LLM
- The research community for developing the RGB framework for hallucination evaluation

---

