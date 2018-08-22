class Date(object):

    def __init__(self, day=0, month=0, year=0):
        self.day = day
        self.month = month
        self.year = year

    @classmethod
    def from_string(cls, date_as_string):
        day, month, year = map(int, date_as_string.split('-'))
        date1 = cls(day, month, year)
        return date1

    @staticmethod
    def is_date_valid(date_as_string):
        day, month, year = map(int, date_as_string.split('-'))
        return day <= 31 and month <= 12 and year <= 3999



So what we must do here is:

Parse a string to receive day, month and year as three integer variables or a 3-item tuple consisting of that variable.
Instantiate Date by passing those values to initialization call.
This will look like:

day, month, year = map(int, string_date.split('-'))
date1 = Date(day, month, year)

# Class Method

    @classmethod
    def from_string(cls, date_as_string):
        day, month, year = map(int, date_as_string.split('-'))
        date1 = cls(day, month, year)
        return date1

date2 = Date.from_string('11-09-2012')
Let's look more carefully at the above implementation, and review what advantages we have here:

We've implemented date string parsing in one place and it's reusable now.
Encapsulation works fine here (if you think that you could implement string parsing as a single function elsewhere, this solution fits OOP paradigm far better).
cls is an object that holds class itself, not an instance of the class. It's pretty cool because if we inherit our Date class, all children will have from_string defined also.


# Static method

What about staticmethod? It's pretty similar to classmethod but doesn't take any obligatory parameters (like a class method or instance method does).

Let's look at the next use case.

We have a date string that we want to validate somehow. This task is also logically bound to Date class we've used so far, but still doesn't require instantiation of it.

Here is where staticmethod can be useful. Let's look at the next piece of code:

    @staticmethod
    def is_date_valid(date_as_string):
        day, month, year = map(int, date_as_string.split('-'))
        return day <= 31 and month <= 12 and year <= 3999

    # usage:
    is_date = Date.is_date_valid('11-09-2012')

And it dont have to be related to self, or cls
