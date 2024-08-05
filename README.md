# Metaprompt

Metaprompt is a Python library for creating and managing meta prompts for various applications. It provides a flexible and extensible framework to define prompts, manage expert roles, and ensure adherence to specific rules and guidelines.

## Installation

To install Metaprompt, use pip:

```bash
pip install https://github.com/deepakgos/metaprompt/releases/download/v1.0.0/metaprompt-1.0.0-py3-none-any.whl
```

## Usage Examples

### MetaPromptingTemplate

The MetaPromptingTemplate class allows you to define and manage expert roles along with their associated descriptions.


```bash
from metaprompt import MetaPromptingTemplate, Expert

# Initialize with the default expert (Meta Expert)
my_instance = MetaPromptingTemplate()
print(f"Selected Expert: {my_instance.expert.name}")
print(f"Expert Description: {my_instance.expert_description}")

# Set a different expert, e.g., Data Analyst
my_instance.set_expert(Expert.DATA_ANALYST)
print(f"Selected Expert: {my_instance.expert.name}")
print(f"Expert Description: {my_instance.expert_description}")
```


### ConfigurationRules

The ConfigurationRules class allows customization of additional rules, response formats, and suggested questions for handling data and queries.


```bash
from metaprompt import ConfigurationRules

# Define suggested questions
sug_ques = [
    'Identify the stores with the highest total inventory levels before sales for each milk brand and day of the week?',
    'What are the total sales and tax amounts for each milk brand on January 1, 2024?'
]

# Define response format guidelines
response_format = """- Present additional details along with the response like Date, Day, Store ID, Store Name, City, Milk Brand, Categories, Quantity of Milk Sold (litres), Price per Litre (Euro), Sales Amount (Euro), Tax Amount (Euro), Inventory Levels (litres) After Sales, and Refill Needed (litres) in a structured format with headings and subheadings.
"""
# Custom examples to be appended
examples = [{
    "examples": [
        {"input": "What is the average sales amount for whole milk in Kretinga?","query": "SELECT AVG(Sales_Amount) FROM MilkSales WHERE City = 'Kretinga' AND Milk_Brand = 'Whole Milk'"},
        {"input": "Find the total quantity of milk sold in each city.","query": "SELECT City, SUM(Quantity_Sold) FROM MilkSales GROUP BY City"}
    ]
}]
# Create a ConfigurationRules instance
configr = ConfigurationRules(
    sug_ques=sug_ques,
    additional_rules=None,
    response_format=response_format
)
```



## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

