## Terraform basics

This document goes through some of the basics of terraform. Every terraform file has an extension `.tf` and uses the following syntax for its members

```
block "label1" label2{
    identifier = expression
}
```

Here,

- `block` is the special keyword or the type of block. For example `output`, `variable`, `modules` etc.
- `label1`&`label2` are the labels of the block
