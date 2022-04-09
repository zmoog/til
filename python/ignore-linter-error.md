# Ignore linter error

Disclaimer: I know, this is pretty basic, but I often forget the exact syntax, so here we are.

Sometimes we want to make a one time exception to a linter error in a specific line of file.

In the following example, we are setting a package description with a little longer value than the project wide settings allows.

Here's how add an exception for the very line:

```python
setup(
    name=NAME,
    version=VERSION,
    description="Python library and a CLI tool to access the https://web.spaggiari.eu",  # noqa: E501
)
```

Adding `noqa: E501` tells flake8 to accept this violation for this line.

Refs:

[Selecting and Ignoring Violations](https://flake8.pycqa.org/en/latest/user/violations.html#in-line-ignoring-errors), from the Flake8 docs.
