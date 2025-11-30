# Code Blocks and Syntax Highlighting

## Inline Code

```typst
Use `variable_name` for inline code.

`#import "module.typ"` is a Typst import.
```

## Code Blocks

### Simple Code Block

```typst
```typst
#let x = 5
#let y = 10
#(x + y)
```
```

Replace `typst` with the language you're using: `python`, `javascript`, `java`, `rust`, `cpp`, `sql`, etc.

### Python Example

```typst
```python
def hello(name):
    print(f"Hello, {name}!")

hello("World")
```
```

### JavaScript Example

```typst
```javascript
function add(a, b) {
  return a + b;
}

console.log(add(5, 3));
```
```

### SQL Example

```typst
```sql
SELECT users.name, COUNT(assignments.id) as task_count
FROM users
JOIN assignments ON users.id = assignments.user_id
GROUP BY users.id;
```
```

## Styled Code Blocks

```typst
#let code_block(content, lang: "plaintext") = block(
  fill: rgb("#f5f5f5"),
  stroke: 1pt + rgb("#cccccc"),
  inset: 10pt,
  text(font: "Courier New", size: 10pt, raw(content))
)

#code_block(
  "fn main() { println!(\"Hello\"); }",
  lang: "rust"
)
```

## Long Code Example

```typst
```javascript
const submitAssignment = async (file) => {
  const formData = new FormData();
  formData.append('file', file);
  
  const response = await fetch('/api/assignments', {
    method: 'POST',
    body: formData,
  });
  
  return response.json();
};
```
```

## Line Numbers

Typst doesn't have built-in line numbers. If you need them, consider:
1. Using an online tool to convert code
2. Adding numbers manually
3. Using a simpler format without highlighting

## Tips

- Language names: `python`, `javascript`, `java`, `rust`, `cpp`, `c`, `sql`, `bash`, `html`, `css`, `typescript`
- Code automatically wraps long lines
- Use backticks for inline code
- Use triple backticks for blocks
- Specify language after opening triple backticks
