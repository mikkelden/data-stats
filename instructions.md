# `README.md` – dbt Test Guidelines

We use dbt with the `clickhouse` dialect.

---

## ✅ Test Guidelines

- Use **only warn-level tests** (`severity: warn`) to avoid breaking production workflows.
- For any non-trivial logic, **add a short inline comment** explaining what the test is doing.
- Avoid `not_null` tests unless nulls would cause actual issues — prefer checks for:
  - Non-empty strings
  - Arrays with at least one item
  - Numeric values greater than zero
- Avoid testing things that are clearly guaranteed by the model logic.
- Do not test business logic assumptions that aren’t visible from the SQL itself.
- Prioritize a few **high-signal tests** over broad test coverage.

---

## 🧪 Custom Tests

- Define custom test macros in `macros/tests/`.
- Reference them in `schema.yml` using `tests: [not_empty_string]` etc.
- Use clear names like `not_empty_string` or `accepted_trigger_types`.
- Avoid abstract macros like `for_all_values()` unless you have a specific reason.
- Custom tests should be reusable, easy to read, and limited in scope.

---

## 🧠 General Principles

- All tests should be understandable at a glance.
- Comment tests that are not obvious.
- Use custom tests when they express intent more clearly than built-ins.
- Be skeptical of tests that require frequent updates without providing real value.
