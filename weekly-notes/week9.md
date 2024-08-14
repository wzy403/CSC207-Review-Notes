### Week 9 Study Notes

## Regular Expressions

### What is a Regular Expression?
**Definition:**
A regular expression (regex) is a sequence of characters that specifies a search pattern in text. It is used for string matching, searching, and text processing.

**Example:**
```regex
\d{3}-\d{2}-\d{4}
```
This regex matches a pattern like a Social Security Number (SSN) in the format "123-45-6789".

### Quantifiers in Regular Expressions
**List of Quantifiers:**
- `*` : Matches 0 or more occurrences of the preceding element.
- `+` : Matches 1 or more occurrences of the preceding element.
- `?` : Matches 0 or 1 occurrence of the preceding element.
- `{n}` : Matches exactly `n` occurrences of the preceding element.
- `{n,}` : Matches `n` or more occurrences of the preceding element.
- `{n,m}` : Matches between `n` and `m` occurrences of the preceding element.

**Example:**
```regex
a{3}
```
This regex matches exactly three consecutive 'a' characters, like "aaa".

### Matching Patterns vs. Repeating Characters
**Difference:**
- **Matching the same pattern multiple times:**
  - Use `{}` to specify the number of times a pattern should be matched.
  - **Example:** `(123){3}` matches "123123123".
- **Repeating the same character multiple times:**
  - Use `\1`, `\2`, etc., to refer back to a `group1 (\1)`, `group2 (\2)`, etc., and repeating that group pattern again.
  - **Example:** `(abc)\1` matches "abcabc".
  - **Example:** `(abc)(123)\1\2` matches "abc123abc123".

### Categorizing Regular Expression Symbols

- **Quantifiers:**
  - Symbols that define the number of times an element must be matched.
  - **Examples:** `*`, `+`, `?`, `{}`

- **Anchors:**
  - Symbols that assert the position in the string.
  - **Examples:** `^` (beginning of the string), `$` (end of the string)

- **Character Classes:**
  - Symbols that define a set of characters to match.
  - **Examples:** `\d` (digits), `\s` (whitespace), `\w` (word characters), `[abc]` (a, b, or c), `[a-z]` (any lowercase letter)

- **Logical Operators and Complement of a Set:**
  - Operators that define logical operations in regex.
  - **Examples:** `|` (or), `&&` (intersection), `[^]` (negated character class)

- **Repetition Symbols:**
  - Symbols that allow repeating parts of the pattern.
  - **Examples:** `*`, `+`, `?`, `{}`

## Disability and Accessibility

### Difficulty in Defining "Disability"
**Explanation:**
Defining "disability" is challenging because it is subjective and varies greatly among individuals. For example, someone with mild color blindness might not consider themselves disabled, but others, including medical professionals, might classify it as a disability. The perception of disability can differ based on personal experiences and societal standards.

### Social Model of Disability
**Definition:**
The social model of disability suggests that limitations are not caused by physical or mental impairments themselves, but by the way these impairments interact with societal structures, including stigma and environmental design.

**Example:**
A person in a wheelchair is not disabled by their condition but by the lack of accessible infrastructure like ramps and elevators.

### Medical Model of Disability
**Definition:**
The medical model of disability views limitations as being caused directly by physical or mental impairments. This model focuses on "fixing" the individual to conform to societal norms.

**Example:**
Treating someone with a hearing impairment through surgery or hearing aids to make them "normal" according to the medical model.

### Insights on Disability and Accessibility
**Learning Reflection:**
Today's lecture provided a new perspective on software UI and interaction design. Previously, I only considered my own experience when developing software. After the lecture, I realized the importance of designing software that meets the needs of all users, not just my own. This includes considering accessibility and the diverse needs of the public.