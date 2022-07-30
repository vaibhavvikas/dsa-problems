## Evaluate the expression

Given a mathematical expression, solve it.

### Google

```bash
input: a-(b+c+b)
output: a-2b-c
```
```bash
input: -(a-(b+c+b)-d-(-(e-b)-d))
output: -a+3b+c-e
```

### Algorithm:

```bash
TC: O(n*n) + O(n) ~> Stack worst case + dict
SC: O(n*n) ~> Stack and dict
```

### Solution

```python
import collections

def sign_converter(sign):
    return "+" if sign == "-" else "-"

def change_sign(expr: str):
    new_subs = ""
    
    if expr[0].isalpha():
        new_subs += "-"
    
    for each in expr:
        if each in ("+", "-"):
            new_subs += sign_converter(each)
        else:
            new_subs += each

    return new_subs

def convert_dict_to_short_string(d):
    res = ""

    for each in d:
        if d[each] == 0:
            continue
        if d[each] < 0:
            if d[each] < -1:
                res += str(d[each]) + each
            else:
                res += "-" + each
        else:
            if d[each] > 1:
                res += "+" + str(d[each]) + each
            else:
                res += "+" + each

    if res[0] == "+":
        return res[1:]
    
    return res


def compress_str(expr_arr):
    d = collections.defaultdict(int)

    for i in range(1, len(expr_arr), 2):
        if expr_arr[i-1] == "+":
            d[expr_arr[i]] += 1
        else:
            d[expr_arr[i]] -= 1
    
    return convert_dict_to_short_string(d)
    

def calculate_expression(expression):
    if expression[0].isalpha():
        expression = "+" + expression

    stack, i = [], 0

    while i < len(expression):
        if expression[i] != ")":
            stack.append(expression[i])
        
        elif expression[i] == ")":
            curr_sub_string = ""
            
            while stack[-1] != "(":
                curr_sub_string += stack.pop()

            curr_sub_string = curr_sub_string[::-1]

            stack.pop()

            if stack and stack[-1] == "-":
                curr_sub_string = change_sign(curr_sub_string)
            
            if curr_sub_string[0].isalpha():
                curr_sub_string = "+" + curr_sub_string

            if stack:
                stack.pop()

            stack += list(curr_sub_string)

        i += 1

    return "".join(stack)


if __name__ == "__main__":
    string = "-(a-(b+c+b)-d-(-(e-b)-d))"
    eval_expr = calculate_expression(string)
    shortened_expr = compress_str(eval_expr)
    print(shortened_expr)
```