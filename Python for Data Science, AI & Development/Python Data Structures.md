# Python: Lists and Tuples

## Tuples
- Tuples are an ordered sequence, expressed as comma-separated elements within parentheses.
- Different types: strings, integer, float can all be contained in a tuple, but the type of the variable is a tuple.
- Elements of a tuple can be accessed via an index (positive or negative).

```python
tuple_example = ("element1", "element2", "element3")
print(tuple_example[0])  # Access first element
print(tuple_example[-1])  # Access last element
```

- Tuples can be concatenated, and sliced.

```python
tuple1 = (1, 2, 3)
tuple2 = (4, 5, 6)
concatenated_tuple = tuple1 + tuple2  # Concatenation
sliced_tuple = concatenated_tuple[0:3]  # Slicing
```

- Tuples are immutable, which means we can't change them.

```python
tuple_example = ("element1", "element2", "element3")
tuple_example[1] = "new_element"  # This will raise an error
```

- Tuples can contain other tuples as well as other complex data types. This is called nesting.

```python
nested_tuple = (("nested1", "nested2"), ("nested3", "nested4"))
```
