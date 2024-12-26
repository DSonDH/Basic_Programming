
# Greatest Common Divisor
```Python3
def gcd(a,b):
""" 유클리드 호제법이라 하며, O(log(N))임. 탐색할 b 범위가 계속 나눠지므로"""
    while b!= 0:
        a,b = b, a%b
    return a
```

# Permutation (not using itertools)

## Permutation non-recursive way
```Python3
def permutations(iterable, r=None):
    # Convert iterable to a tuple to ensure immutability 
    pool = tuple(iterable)
    n = len(pool)
    r = n if r in None else r

    if r > n:
        return

    indices = list(range(n))
    cycles = list(range(n, n - r, -1))

    yield tuple(pool[i] for i in indices[:r])
    while n:
        for i in reversed(range(r)):
            cycles[i] -= 1
            if cycles[i] == 0:
                # Rotate indices
                indices[i:] = indices[i + 1:] + indices[i : i + 1]
                cycles[i] = n - i

            else:
                j = cycles[i]
                indices[i], indices[-j] = indices[-j], indices[i]
                yield tuple(pool[i] for i in indices[:r])
                break
        else:
            return
```
### Permutation non-recursive way; not using yield
```Python3
def permutations(iterable, r=None):
    # Convert the iterable to a list
    pool = list(iterable)
    n = len(pool)
    r = n if r is None else r

    if r > n:
        return []

    # Result list to store all permutations
    result = []

    # Initial indices for generating permutations
    indices = list(range(n))
    cycles = list(range(n, n - r, -1))

    # Append the first permutation
    result.append(tuple(pool[i] for i in indices[:r]))

    while n:
        for i in reversed(range(r)):
            cycles[i] -= 1
            if cycles[i] == 0:
                # Rotate indices[i:] to the left
                indices[i:] = indices[i+1:] + indices[i:i+1]
                cycles[i] = n - i
            else:
                j = cycles[i]
                indices[i], indices[-j] = indices[-j], indices[i]
                result.append(tuple(pool[i] for i in indices[:r]))
                break
        else:
            break

    return result
```


## Permutation recursive way
```Python3
def permutation(iteravle, r = None):
    # Convert iterable to a tuple to ensure immutability
    pool = tuple(iterable)
    n = len(pool)
    r = n if r is None else r

    if r > n:
        return

    # Helper function to generate permutations recursively
    def generate(current, remaining):
        if len(current) == r:
            yield tuple(current)
        else:
            for i in range(len(remaining)):
                # Pick the i-th element and continue with the rest
                yield from generate(current + [remaining[i]], remaining[:i] + remaining[i + 1:])

    yield from generate([], list(pool))    
```

### Permutation recursive way; not using yield
```Python3
def permutations(iterable, r=None):
    # Convert the iterable to a tuple
    pool = tuple(iterable)
    n = len(pool)
    r = n if r is None else r

    if r > n:
        return []

    # Result list to store all permutations
    result = []

    # Recursive helper function
    def generate(current, remaining):
        if len(current) == r:
            result.append(tuple(current))
        else:
            for i in range(len(remaining)):
                # Choose the i-th element and recurse with the rest
                generate(current + [remaining[i]], remaining[:i] + remaining[i+1:])

    # Start the recursive process
    generate([], list(pool))

    return result
```
