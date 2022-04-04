# Dunder Methods
special methods are predefined methods to enrich classes , these methods starts and ends with  double underscores , like __init__ and __str__

the term "dunder" is used to refer to these methods as a short form of "double under"

here is some of these methods:

__len__ : you use this to check the length of a class , it iterates over the instances of the class

__init__ : this method to start the class. it construct the objects in the form of this class.

__srt__ : The “informal” or nicely printable string representation of an object. This is for the enduser.

__repr__ :The “official” string representation of an object. This is how you would make an object of the class

__getitem__ : it return the instances in the class.

__reversed__ : it will return the instances in reversed order

__add__ : to add class instances together

__call__ : this to make an object callable like a regular function .

**strategic use of dunder methods makes classes more Pythonic.** 

-----------
# Statistics and Probability

probability in simple words is what is the chance of an event to happen.To calculate the chance of an event happening, we also need to consider all the other events that can occur. 

to get close what probabilty wants , we need to get statistics by trials. they higher the number of trials the closer we are to the predicted probability . 
like in the coin toss trials . we expect the head to be appear 50% of the tosses. which we came close to if we increas the numbers of trials. in
lower trials , the numbers will not be so close to predicted .Thus, given enough data, statistics enables us to calculate probabilities using real-world observations. Probability 
provides the theory, while statistics provides the tools to test that theory using data. The descriptive statistics, specifically mean and standard deviation, become the proxies for the 
theoretical.
## The data and the distribution
normal distribution has its own shape , it represents the normal figure data will fall under and draw when represnted.
we can use what called the three sigma rule , which is an expression of how many of our observations fall within a certain distance of the mean.
the standard deviation is the average distance an observation in the data set is from the mean. The Three Sigma rule dictates that given a normal distribution, 68% of your observations will fall between one standard deviation of the mean. 95% will fall within two, and 99.7% will fall within three.

The Z-score is a simple calculation that answers the question, “Given a data point, how many standard deviations is it away from the mean?”
By itself, the Z-score doesn’t provide much information to you. It gains the most value when compared against a Z-table, which tabulates the cumulative probability 
of a standard normal distribution up until a given Z-score. A standard normal is a normal distribution with a mean of 0 and a standard deviation of 1. The Z-score lets us reference this the Z-table even if our normal distribution is not standard. The cumulative probability is the sum of the probabilities of all
values occurring, up until a given point.


## Conclusion

We started with descriptive statistics and then connected them to probability. From probability, we developed a way to quantatively show if two groups come from the same distribution. In this case, we compared two wine recommendations and found that they most likely do not come from the same score distribution.
In other words, one wine type is most likely better than the other one. Statistics doesn’t have to be a field relegated to just statisticians. As a data scientist, having an intuitive understanding on common statistical measures represent will give you an edge on developing your own theories and the ability to
subsequently test these theories. We barely scratched the surface of inferential statistics here, but the same general ideas here will help guide your intuition in your statistical journey. Our article discussed the advantages of the normal distribution, but statisticians have also developed techniques to adjust for 
distributions that aren’t normal.

