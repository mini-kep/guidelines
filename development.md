# Testing

  See [testing requirements and guidelines](https://github.com/mini-kep/guidelines/blob/master/testing.md).


# Docstrings

Following parts of code should have docstrings:
- critical parts of the code that do something really important
- parts of the code that are exposed to end-user

When writing a docstring stick to [Google style](https://google.github.io/styleguide/pyguide.html#Comments).

When constrained on time:
1. write one liner docstring
2. write a part of docstring which is has most information (usually `Args` section)
3. finish a docstring after review

# Branches

- Creating branches in repo is preferred to branches in forks.
- Reference branch  is `dev` - branch out and make PRs to it. 

## Branch naming

1. Use prefix:
   - `dev` (feature, enhancement), use this when in doubt
   - `fix` (bugs, bad behavior)
   - `test` (working on tests exclusively)   
2. Put a few words inside 
3. Postfix with issue number 
4. Use `-` to separate 

Pattern: ```dev-something-something-10```

Examples:

- ```dev-compress-dataset-71```
- ```fix-large-dataset-fault-10```
- ```test-csv-serialialiser-2```

# Github identity 

Github avatar and username are very personal things, 
but it (subjectively) makes life easier, if:

- avatar is distiguishable from others:
  - not a standard avtar, like all others
  - not a greyish/brownish picture, like all others
  
- username has some association to who you are, unless disambiguation is intentional

- a memorable, short and easy to type username is better  
  
