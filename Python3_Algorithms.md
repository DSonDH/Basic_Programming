
# Greatest Common Divisor
```Python3
def gcd(a,b):
""" 유클리드 호제법이라 하며, O(log(N))임. 탐색할 b 범위가 계속 나눠지므로"""
    while b!= 0:
        a,b = b, a%b
    return a
```

# Permutation (not using itertools)

```Python3
def permutations(iterable, r=None):
    """
    iterable을 리스트로 변환하여 인덱스를 조작하기 쉽게 만듦.
    indices는 순열을 생성하기 위해 요소의 인덱스를 관리.
    cycles는 각 자리에 대해 회전 횟수를 기록.
    """
    pool = list(iterable)
    n = len(pool)
    r = n if r is None else r

    if r > n:
        return []

    result = []
    indices = list(range(n))
    cycles = list(range(n, n - r, -1))

    result.append(tuple(pool[i] for i in indices[:r]))

    print("i,   indices,    cycles")
    print(None, indices, cycles)
    while True:
        for i in reversed(range(r)):
            # 2, 2, 1, 2, 2, 1, 2, 2, 1, 0 반복되고 있음
            cycles[i] -= 1  # 이걸 먼저 빼는게 맞는건가

            if cycles[i] == 0:
                # Rotate indices[i:] to the left
                indices[i:] = indices[i + 1 :] + indices[i : i + 1]

                cycles[i] = n - i

                print(i, indices, cycles, "c1")
            else:
                # TODO: 이게 어떻게 일반화된 n개 요소에 대해 동작하는지 이해하고싶음
                j = cycles[i]
                indices[i], indices[-j] = indices[-j], indices[i]  # Swap

                result.append(tuple(pool[i] for i in indices[:r]))

                print(i, indices, cycles, "c2")
                break
        else:
            break

    return result


def permutations2(iterable, r=None):
    pool = sorted(iterable)
    n = len(pool)
    r = n if r is None else r

    if r > n:
        return []

    # Generate permutations in lexicographical order
    result = []
    while True:
        # Append the first r elements as a tuple
        result.append(tuple(pool[:r]))

        # Step 1: Find the largest index k such that pool[k] < pool[k + 1]
        k = -1
        for i in range(n - 1):
            if pool[i] < pool[i + 1]:
                k = i

        # If no such index exists, we are at the last permutation
        if k == -1:
            break

        # Step 2: Find the largest index l such that pool[k] < pool[l]
        for l in range(n - 1, k, -1):
            if pool[k] < pool[l]:
                # Step 3: Swap pool[k] and pool[l]
                pool[k], pool[l] = pool[l], pool[k]
                break

        # Step 4: Reverse the sequence from pool[k + 1] to the end
        pool = (
            pool[: k + 1] + pool[k + 1 :][::-1]
        )  # 이거 안하면 결과 다 안나오네? 중요한 코드임
        print(pool)

    return result


def permutations3(iterable, r=None):
    pool = list(iterable)
    n = len(pool)
    r = n if r is None else r

    if r > n:
        return []

    result = []
    stack = [0] * n  # Stack to simulate the recursion
    current_perm = pool[:]  # Working list to generate permutations

    result.append(tuple(current_perm[:r]))  # Add initial permutation
    print(result)

    i = 0  # Pointer to the current position
    while i < n:
        if stack[i] < i:  # Generate permutations based on stack
            if i % 2 == 0:
                swap_index = 0
            else:
                swap_index = stack[i]

            current_perm[i], current_perm[swap_index] = (
                current_perm[swap_index],
                current_perm[i],
            )
            print(current_perm)
            result.append(tuple(current_perm[:r]))
            
            stack[i] += 1
            i = 0  # Reset pointer to start over
        else:
            stack[i] = 0
            i += 1  # Move to the next level

    return result


# Test the function with an example
iterable = "ABCD"
r = 3

# results = permutations(iterable, r)
# print(results)

results2 = permutations2(iterable, r)
print(results2)

results3 = permutations3(iterable, r)
print(results3)

# assert set(results) == set(results2)
# assert set(results2) == set(results3)
```



## Permutation non-recursive way
```Python3
def permutations(iterable, r=None):
    """
    iterable을 리스트로 변환하여 인덱스를 조작하기 쉽게 만듦.
    indices는 순열을 생성하기 위해 요소의 인덱스를 관리.
    cycles는 각 자리에 대해 회전 횟수를 기록.
    """

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
    """
    iterable을 리스트로 변환하여 인덱스를 조작하기 쉽게 만듦.
    indices는 순열을 생성하기 위해 요소의 인덱스를 관리.
    cycles는 각 자리에 대해 회전 횟수를 기록.
    """

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
    """
    iterable을 리스트로 변환하여 인덱스를 조작하기 쉽게 만듦.
    indices는 순열을 생성하기 위해 요소의 인덱스를 관리.
    cycles는 각 자리에 대해 회전 횟수를 기록.
    """
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
    """
    iterable을 리스트로 변환하여 인덱스를 조작하기 쉽게 만듦.
    indices는 순열을 생성하기 위해 요소의 인덱스를 관리.
    cycles는 각 자리에 대해 회전 횟수를 기록.
    """
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
