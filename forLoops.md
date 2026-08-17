total = 0; # container

for value in [3 ,2 ,19]:  # For loop iterating over a list
    total += value # += operator to add value to total

print('Total is: {0} '.format(total))

# create a vector of words
words = ['Python', 'is', 'fun']

# A for loop that iterates over the words in the list using an index.
for i in range(len(words)):
    print('Word {0} is: {1}'.format(i, words[i]))

#weighted average 
X = [2 ,3 ,19]
p = [0.2 ,0.3 ,0.5]

total = 0
for i in range(len(X)):
    total += p[i] * X[i]
print('Weighted average is: {0} '.format(total))
