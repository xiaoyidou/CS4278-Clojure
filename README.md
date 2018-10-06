# Dinner Decisions

This project will involve using a text messaging interface similar to Uber/Lyft's
auto-reply system for resolving customer complaints to help a user decide which restaurant
to eat based on the user's preferences. The structure of the application will involve the 
text messaging framework we have developed so far. A user will be able to provide the
application with texts of their preferences, representing attributes of restaurants (cheap,
Chinese, no pizza, etc.) and the application will eliminate and prioritize restaurants based
on the labels. From the interviews, several important features will be implemented based on
client needs.

From the interviews, it was discovered that most clients will come up with a decision for 
where to have dinner with their friends. Thus, it would be beneficial to have groups in
this application, where multiple users can have inputs toward the decision. It may also
be interesting to have users within a group weighted differently. It also seems to take quite
a while for people to decide where to eat out, so a need for streamlining this process is
desirable. It is important for the application to follow the usual strategy we do: eliminate
restaurants we don't like and prioritize the ones we do like. It also seems like displaying
a list of restaurants that fit the constraints will get the job done.

Being able to have decision support software in multiple areas of your life is a move toward
the future. If this application is successful, it may be more useful to cache user data and
use historical data for groups to make better suggestions for restaurants. It also may be 
helpful to make a more sophisticated filtering technique that is not so binary (eliminated/not
eliminated). Perhaps machine learning approaches could be used to take in the labels and filter
for restaurants based on the probability it fits the criteria and be trained on the feedback
given after each run.

# Questions:

1.	How do you decide what to get for dinner when the food on campus in not up to par?
2.	How long does it usually take to decide on where to get delivery from or where to go out for dinner?
3.	How frustrating is the process as a whole?
4.	Do you usually come to a conclusion with other friends or by yourself?
5.	Is the usual strategy to eliminate the places you don’t like first?
6.	Would it be desirable to automate the process of deciding on a meal?
7.	What kind of features would you expect?
8.	Would you be satisfied with something like Uber/Lyft’s automatic messaging system?
9.	Would you be willing to let the app keep a history of your conversations for improving suggestions?
10.	What other aspects of life would you consider “decision making assistance” apps helpful towards?

# Answers:

## Question 1:

1.	"I will ask my friends to see if someone wants to eat off campus or order delivery with me."
2.	"I ask my friends"
3.	"Figure out what restaurants are on the Commodore card"

## Question 2:

1.	"10 minutes"
2.	"20 minutes"
3.	"30 minutes"

## Question 3:

1.	"If I couldn’t find any accompany after several attempts I’ll be very depressed and may end up skipping the dinner."
2.	"Fairly frustrating"
3.	"5 ouf of 10"

## Question 4:

1.	"With other friends."
2.	"With friends"
3.	"Myself"

## Question 5:

1.	"No. I usually check my favorite places first."
2.	"Sometimes yeah"
3.	"yes"

## Question 6:

1.	"Yes."
2.	"Sure"
3.	"yes"

## Question 7:

1.	"Optimizing the restaurant choice list by processing my eating habits and dinner history, and explore new popular restaurants as additional choices."
2.	"Not entirely sure, maybe just a list of restaurants that fit in a given category"
3.	"Ability to get a list of restaurants that use the Commodore card"

## Question 8:

1.	"No. Sending message to decide the place for dinner would be time-consuming and inefficient."
2.	"Sure"
3.	"yes"

## Question 9:

1.	"Yes."
2.	"Yes."
3.	"yes"

## Question 10:

1.	"Online shopping. Sometimes it is hard to find the appropriate product and a “decision making assistance” app would be very helpful in searching for the best product."
2.	"Deciding when it's worth it to go to class"
3.	"What meals to prepare on your own"

# Requirements

1.	The application must have an interface that stores user preferences in the form of
strings and maintain an internal database of users and their preferences.
2.	Strings must follow a standard format associated with an action and a descriptor.
For example, "less_than _descriptor_" will filter for restaurants that have an average price
less than _descriptor_. "no _descriptor_" will filter for restaurants that are not associated
with _descriptor_.
3.	The application must contain a database of restaurants and their attributes, which will
either be collected through web scraping or through accessing an API that stores such
information (e.g. Yelp).
4.	The application must be able to handle input from multiple people in the same group.
Because people often times order with friends, it would be nice if multiple people could
send input to the application to parallelize the task. However, their input must only affect
the recommendation for that group.

# Development Approach

1.	The application will use the existing state-mgr framework already implemented in our
assignments to map users to their preferences.
2.	The application will route commands to their functions in a similar way to the experts
register and query demo already implemented in our assignments.
3.	User preferences and the restaurant database will be kept as separate state-mgr objects.
They will each have their own set of protocols for adding users, adding preferences, and
creating groups. The restaurant database will have its own set of protocols for adding 
restaurants, looking up restaurants, and querying for other data.
4.	Parsers must be created to make sure that the command exists and that the associated
_descriptor_ is a valid argument for the command.
5.	A nice visualization of the list of candidate restaurants at any point in time must
be made in order to display results back to the users.
6.	Getting data from the source will prove to be a big obstacle in this project. Currently,
Yelp does not support a Clojure API, but an open source one is available (though it looks) 
like it has been dead since 2016. Hopefully it is usable.