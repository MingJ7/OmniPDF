# OmniPDF Python Style Guide

# Introduction
This style guide outlines the coding conventions for Python code developed for OmniPDF.
Please use PEP8.

# Key Principles
* **Readability:** Code should be easy to understand for all team members.
* **Maintainability:** Code should be easy to modify and extend.
* **Consistency:** Adhering to a consistent style across all projects improves
  collaboration and reduces errors.
* **Performance:** While readability is paramount, code should be efficient.

# Gemini Guides
* **Comment Piority** Comments should be posted in order of severity, starting with CRITICAL, HIGH, MEDIUM and finally LOW. All comments of higher severity must be posted before a comment of lower severity is posted.
* **Naming Conventions** Comments regarding naming conventions should be collated together by file. Each file should only have 1 comment for all naming convention changes to be made. 
* **Comment Format** Comments should follow the following example:
```markdown
![critical](https://www.gstatic.com/codereviewagent/critical.svg)
## \[ACTION NEEDED\] Correctness

The `service_cache.add()` and `service_cache.remove()` methods are called with only `doc_id` as an argument. However, the `ServiceCache.add` and `ServiceCache.remove` methods in `shared_utils/redis.py` are defined to accept two arguments: `key` and `value` (e.g., `def add(self, key: str, value: str):`).

Calling them with only one argument (e.g., `service_cache.add(doc_id)`) will result in `doc_id` being passed as the `key`, and the `value` argument will be missing, leading to a `TypeError` at runtime.

The `service_cache.contains(__name__, doc_id)` call on line 34 correctly uses `__name__` as the key and `doc_id` as the value. The `add` and `remove` calls should follow this pattern.

\`\`\`suggestion
    if req.status_code == 202 and not doc_is_processing:
        service_cache.add(__name__, doc_id)  # Pass __name__ as key and doc_id as value
    elif req.status_code == 200 and doc_is_processing:
        service_cache.remove(__name__, doc_id)  # Pass __name__ as key and doc_id as value
\`\`\`
```