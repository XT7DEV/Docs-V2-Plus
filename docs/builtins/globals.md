---
title: Global Functions
description: Documentation on global functions for luau
weight: 1
---

### assert

```lua
assert(t: any, message: string?): any
```

This function checks if the value `t` is equivalent to true and will return true if it is. If it is not however, it will raise an error. The error message can be customized with an optional parameter `message`.

**Examples**

```lua
local product = 5 * 5
assert(product == 25, "The math is dead")
```

This will do nothing because 5 x 5 is 25

```lua
local product = 5 * 5
assert(product == 55, "The math is dead")
```

This on the other hand will raise an error `The math is dead` because 5 x 5 does not equal 55

---

### error

```lua
error(obj: any, level: number?)
```

When called `error` will raise an error (duh) with the specified object `obj`.
When `level` is specified, the error raised is turned into a string that contains call frame information for the caller at level `level`, where `1` refers to the function that called `error`. This can be useful to attribute the errors to callers, for example `error("Expected a valid object", 2)` highlights the caller of the function that called `error` instead of the function itself in the callstack.

**Example**

```lua
error("Hunger stole my cookies", 1)
```

This throws an error `Hunger stole my cookies` with a level of 1

---

### gcinfo

```lua
gcinfo(): number
```

`gcinfo` returns the total heap size in kilobytes. The number returned by `gcinfo` reflects the current heap
consumption from the operating system perspective and can fluctuate over time as garbage collector frees objects.

**Example**

```lua
local value = gcinfo()
print(value)
```

---

### getfenv

<div data-search-exclude markdown>

!!! warning "Warning!"
    This can introduce security vulnerabilities! Use at your own risk!

</div>

```lua
getfenv(target: (function | number)?): table
```

Returns the environment table for target function; when `target` is not a function, it must be a number corresponding to the caller stack index, where 1 means the function that calls `getfenv`, and the environment table is returned for the corresponding function from the call stack. When `target` is omitted it defaults to `1`, so `getfenv()` returns the environment table for the calling function.

**Example**

```lua
local funcenv = getfenv(1)
print(funcenv)
```

This will return the environment table for target function which in this case is the script

---

### getmetatable

```lua
getmetatable(obj: any): table?
```

Returns the metatable for the specified object; when object is not a table or a userdata, the returned metatable is shared between all objects of the same type.

<div data-search-exclude markdown>

!!! note "Note:"
    When metatable is protected (has a `__metatable` key), the value corresponding to that key is returned instead and may not be a table.

</div>

**Example**

```lua
local metatbl = {}
local tbl = setmetatable({}, metatbl)
print(getmetatable(tbl) == metatbl) --> true

-- Make the original metatable unrecoverable by setting the __metatable metamethod:
metatbl.__metatable = "protected"
print(getmetatable(tbl)) --> protected
```

---

### ipairs

```lua
ipairs(t: table): <iterator>
```

Returns the triple (generator, state, nil) that can be used to traverse the table using a `for` loop. The traversal results in key-value pairs for the numeric portion of the table; key starts from 1 and increases by 1 on each iteration. The traversal terminates when reaching the first `nil` value (so `ipairs` can't be used to traverse array-like tables with holes).

**Example**

```lua
local elements = {"hydrogen", "lead", "iron"}
for index, element in ipairs(elements) do
   print(index, element) --> 1 hydrogen, 2 lead, 3 iron, etc...
end
```

---

### next

```lua
next(t: table, i: number?): (K, V)?
```

Given the table `t`, returns the next key-value pair after `i` in the table traversal order, or nothing if `i` is the last key. When `i` is `nil`, returns the first key-value pair instead.

**Example**

```lua
function clone (t)           -- t is a table
  local new_t = {}           -- create a new table
  local i, v = next(t, nil)  -- i is an index of t, v = t[i]
  while i do
    new_t[i] = v
    i, v = next(t, i)        -- get next index
  end
  return new_t
end

clone({"Hi"})
```

---

### newproxy

```lua
newproxy(mt: boolean?): userdata
```

Creates a new untyped userdata object; when `mt` is true, the new object has an empty metatable that can be modified using `getmetatable`.

---

### pairs

```lua
pairs(t: table): <iterator>
```

Returns the triple (generator, state, nil) that can be used to traverse the table using a `for` loop. The traversal results in key-value pairs for all keys in the table, numeric and otherwise, but doesn't have a defined order.

**Example**

```lua
local testscores = {
    ["Bags"] = "A",
    ["Leo"] = "F"
}

for name, score in pairs(testscores) do
    print(name .. " has score: " .. score)
end
```

---

### pcall

```lua
pcall(f: function, args: ...any): (boolean, ...any)
```

Calls function `f` with parameters `args`. If the function succeeds, returns `true` followed by all return values of `f`. If the function raises an error, returns `false` followed by the error object.
Note that `f` can yield, which results in the entire coroutine yielding as well.

**Example**

```lua
local function divideBySeven(n: number): number
	return n / 7
end

local success, msg = pcall(divideBySeven, "DefinitelyANumber")  -- Results in error...

if success then
	-- Logic for successful response...
else
	print("Error message:", msg)
end
```

---

### print

```lua
print(args: ...any)
```

Prints all arguments to the standard output, using Tab as a separator.

**Example**

```lua
print("Hello World")
```

---

### rawequal

```lua
rawequal(a: any, b: any): boolean
```

Checks whether `a` is equal to `b`, without invoking any metamethods.

---

### rawget

```lua
rawget(t: table, k: number): number?
```

Performs a table lookup with index `k` and returns the resulting value, if present in the table, or nil. This operation bypasses metatables/`__index`.

---

### rawlen

```lua
rawlen(t: table | string): number
```

Returns the raw length of the table or string. If it is a string, this operation is identical to `#str` or `string.len(str)`. This operation bypasses metatables/`__len`.

---

### rawset

```lua
rawset(t: table, k: any, v: any)
```

Assigns table field `k` to the value `v`. This operation bypasses metatables/`__newindex`.

---

### select

```lua
select(i: string, args: ...T): number
select(i: number, args: ...T): ...T
```

When called with `'#'` as the first argument, returns the number of remaining parameters passed. Otherwise, returns the subset of parameters starting with the specified index.
Index can be specified from the start of the arguments (using 1 as the first argument), or from the end (using -1 as the last argument).

---

### setfenv

<div data-search-exclude markdown>

!!! warning "Warning!"
    This can introduce security vulnerabilities! Use at your own risk!

</div>

```lua
setfenv(target: function | number, env: table)
```

Changes the environment table for target function to `env`; when `target` is not a function, it must be a number corresponding to the caller stack index, where 1 means the function that calls `setfenv`, and the environment table is returned for the corresponding function from the call stack.

---

### setmetatable

```lua
setmetatable(t: table, mt: table?)
```

Changes metatable for the given table. Note that unlike `getmetatable`, this function only works on tables. If the table already has a protected metatable (has a `__metatable` field), this function errors.

---

### tonumber

```lua
tonumber(s: string, base: number?): number?
```

Converts the input string to the number in base `base` (default 10) and returns the resulting number. If the conversion fails (that is, if the input string doesn't represent a valid number in the specified base), returns `nil` instead.

**Example**

```lua
print(tonumber("1984")) --> 1984 (assumes base 10, decimal)
print(tonumber("1.27")) --> 1.27 (base 10 may have decimal portions)
print(tonumber("3e5")) --> 300000 (base 10 may have scientific notation, 3 x 10 ^ 5)
print(tonumber("25", 8)) --> 21 (base 8, octal)
print(tonumber("0x100")) --> 256 (assumes base 16, hexadecimal)
print(tonumber("polytoria")) --> nil (does not raise an error)

-- Tip: use assert if you would like strings that cant be converted to numbers to raise an error
print(assert(tonumber("polytoria"))) --> Error: assertion failed
```

---

### tostring

```lua
tostring(obj: any): string
```

Converts the input object to string and returns the result. If the object has a metatable with `__tostring` field, that method is called to perform the conversion.

**Example**

```lua
local PolytoriaIsAwesome = true
print("Polytoria is Awesome: " .. tostring(PolytoriaIsAwesome)) --> Polytoria is Awesome: true
```

---

### type

```lua
type(obj: any): string
```

Returns the type of the object, which is one of `"nil"`, `"boolean"`, `"number"`, `"vector"`, `"string"`, `"table"`, `"function"`, `"userdata"`, `"thread"`, or `"buffer"`.

**Example**

```lua
local str = "This is a string"
print(type(str)) --> string
```

---

### unpack

```lua
unpack(a: table, f: number?, t: number?): ...any
```

Returns all values of `a` with indices in `[f..t]` range. `f` defaults to 1 and `t` defaults to `#a`. Note that this is equivalent to `table.unpack`.

---

### xpcall

```lua
xpcall(f: function, e: function, args: ...any): (boolean, ...any)
```

Calls function `f` with parameters `args`. If the function succeeds,  returns `true` followed by all return values of `f`. If the function raises an error, calls `e` with the error object as an argument, and returns `false` followed by the first return value of `e`.
Note that `f` can yield, which results in the entire coroutine yielding as well.
`e` can neither yield nor error - if it does raise an error, `xpcall` returns with `false` followed by a special error message.
