# **Natural Language to SQL Query Generation using LangChain and Comparing Various Promting Techniques(Zero-Shot, Few-Shot, COT, Self-Consistency) **

## **1. Introduction**
This project focuses on converting natural language (NL) questions into structured SQL queries using large language models (LLMs) with LangChain. The dataset used is from Kaggle, and PostgreSQL is employed for database management. The project explores various prompting techniques such as Zero-Shot, Few-Shot, Chain-of-Thought, and Self-Consistency to optimize query generation accuracy.

## **2. Dataset Processing**
### **Downloading and Processing Kaggle Dataset**
1. The dataset was sourced from Kaggle and downloaded using the Kaggle API.
2. The data was cleaned, formatted, and loaded into a PostgreSQL database.
3. The schema was designed with proper constraints and descriptive column comments for clarity.

## **3. PostgreSQL Schema Design**
The PostgreSQL schema was structured to reflect an Airbnb-like database containing `listings` and `reviews` tables. Each column was assigned a meaningful data type and detailed comments to enhance LLM understanding.

### **Listings Table**
```sql
-- Table: listings
-- listing_id: BIGINT, unique identifier for each listing.
-- name: TEXT, name/title of the listing.
-- host_id: BIGINT, unique identifier for the host.
-- price: DECIMAL, price per night.
-- city: TEXT, city of the listing.
-- review_scores_rating: FLOAT, overall rating.
```

### **Reviews Table**
```sql
-- Table: reviews
-- review_id: SERIAL PRIMARY KEY, unique identifier for each review.
-- listing_id: INTEGER, foreign key linking to listings(listing_id).
-- date: DATE, date when the review was posted.
-- reviewer_id: INTEGER, unique identifier for the reviewer.
```

## **4. Hugging Face LLM Setup**
1. A Hugging Face account was created.
2. An API token was generated and used to access hosted models.
3. An appropriate text-based LLM was selected for NL-to-SQL conversion.

## **5. LangChain Prompt Engineering Methodology**
LangChain was used to structure and refine prompt templates, exploring various prompting techniques:

### **Zero-Shot Prompting**
- Relied solely on the model's generalization capabilities without any examples.
- Provided only schema details and NL queries.

### **Few-Shot Prompting**
- Included examples of correct NL-to-SQL conversions.
- Example:
  ```
  NL Query: "Get all listings in New York City."
  SQL: SELECT * FROM listings WHERE city = 'New York City';
  ```

### **Chain-of-Thought (CoT) Prompting**
- Encouraged intermediate reasoning steps before generating SQL.
- Example reasoning steps:
  - Identify tables involved.
  - Determine relevant columns.
  - Construct SQL query logically.

### **Self-Consistency Prompting**
- Generated multiple SQL queries.
- Used an aggregation method to select the most accurate query.

## **6. Evaluation of SQL Generation**
### **Running and Validating Queries**
- Queries were executed against a PostgreSQL instance.
- Outputs were checked for correctness against expected results.

### **Evaluation Criteria**
1. **Correctness:** Did the SQL query return expected results?
2. **Efficiency:** Was the generated SQL query optimized?
3. **Prompt Effectiveness:** Did schema comments and structured prompts improve accuracy?
4. **Integration Quality:** Did LangChain seamlessly generate and execute queries?

## **7. Conclusion**
This project demonstrated how effective prompt engineering techniques significantly enhance the accuracy of LLM-generated SQL queries. Future work could explore fine-tuning models for domain-specific SQL generation and optimizing query efficiency.

---


