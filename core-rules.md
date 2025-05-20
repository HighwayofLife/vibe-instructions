# Core Principles

1. **KISS (Keep It Simple, Stupid):** Prioritize straightforward solutions over complex ones. Avoid overengineering unless explicitly required by the problem.
2. **DRY (Don’t Repeat Yourself):** Extract reusable logic into functions, classes, or modules. Replace duplicated code with shared utilities.
3. **SOLID Compliance:**  
   - **Single Responsibility:** Each function/class should have one purpose.  
   - **Open/Closed:** Design code to be extensible without modification.  
   - **Liskov Substitution:** Subtypes must be interchangeable with base types.  
   - **Interface Segregation:** Avoid bloated interfaces; split into focused ones.  
   - **Dependency Inversion:** Depend on abstractions, not concretions.

4. **Law of Demeter:**  
   Minimize dependencies between components. Objects should only interact with direct collaborators.

---

### Code Quality & Readability
5. **Adhere to Language-Specific Style Guides**  
   - Use linters/formatters (e.g., `black` for Python, `Prettier` for JS) for consistent indentation, line length (80–120 chars), and brace placement.  
   - Example:  
     ```python
     # Bad
     def c(a,b):return a*b
     # Good
     def calculate_pay(hours: float, rate: float) -> float:
         return hours * rate
     ```

6. **Descriptive Naming Conventions**  
   - Use `snake_case`/`CamelCase` as per language norms. Avoid abbreviations.  
   - Example:  
     ```python
     # Bad
     def fn(a, b): ...
     # Good
     def calculate_weekly_revenue(orders: list, price: float) -> float: ...
     ```

7. **Effective Commenting**  
   - Explain "why" for complex logic, not "what." Avoid redundant comments.  
   - Use tools like Better Comments for standardization.

---

### AI-Specific Guidelines
8. **Explicit Requirements**  
   - Specify language, frameworks, and constraints in prompts (e.g., *"Use Python 3.12 with type hints and pytest for testing"*).

9. **Modular Design**  
   - Break tasks into small, testable functions. Favor composition over inheritance.  
   - Example:  
     ```python
     # Bad: Monolithic function
     def process_data():
         # 100 lines of mixed I/O, parsing, and calculations
     # Good: Modular
     def load_data(path: str) -> list: ...
     def clean_data(raw: list) -> pd.DataFrame: ...
     ```

10. **Error Handling & Testing**  
    - Include try/except blocks and edge-case tests. Generate unit tests for critical paths.  
    - Example:  
      ```python
      def divide(a: float, b: float) -> float:
          if b == 0:
              raise ValueError("Denominator cannot be zero")
          return a / b
      ```

---

### Security & Maintenance
11. **Security-First Code**  
    - Sanitize inputs, avoid hardcoded secrets, and use parameterized queries.

12. **Document AI Usage**  
    - Add metadata tags (e.g., `# AI-Generated`) and track changes made post-generation.

13. **Performance Optimization**  
    - Vectorize operations, limit loops, and profile bottlenecks.  
    - Example (Python):  
      ```python
      # Bad: Nested loops
      for i in list_a:
          for j in list_b: ...
      # Good: Vectorized
      result = np.array(list_a) * np.array(list_b)
      ```

---

### Workflow Integration
14. **Pre-Review Validation**  
    - Require manual review and static analysis (e.g., SonarQube) before merging AI-generated code.

15. **Iterative Refinement**  
    - Use feedback loops: Generate → Review → Refine → Repeat.

16. **Avoid Over-Reliance**  
    - Use AI for boilerplate/routine tasks, not critical architecture.
