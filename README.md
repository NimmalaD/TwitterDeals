## Assignment Two - Scraping Twitter 

**Members:**

Shruti Milind Randive, 
Amretasre Rengarajan Thiruvengadam, 
Sraddha Pedda Gangireddy Gari, 
Dharma Thanishq Nimmala.

**Introduction:**

This database contains tweets tweeted by users for deals offered by various retailers such as Walmart, Target, and Sam’s Club. Tweets have been scrapped from Twitter based on hashtags and keywords related to Black Friday and Thanksgiving deals for specific retailers. The tables have been split into user Twitter details and tweet details. Each tweet will have a unique tweet id, similarly, each user will have a unique user id. The tables have been designed concerning these ids. The URLs, Hashtags, and Mentions in each tweet have been added to different tables for each retailer.

**Conceptual Model:**

![twitter UML](https://user-images.githubusercontent.com/114887817/201502663-478879e7-f004-44d1-be37-b17eae4dfd16.jpeg)


**Physical Model:**
 **
1. Queries to Create Tables:** 

CREATE DATABASE twitterdeals
User Table
CREATE TABLE twitter_users(
    user_id BIGINT(20),
    user_name TEXT,
    follower_count BIGINT(20),
    friend_count BIGINT(20),
    user_profile_img TEXT, 
    descriptions TEXT
    user_created_at TEXT,
    tweet_id BIGINT(20),
    PRIMARY KEY  (user_id )
);

Walmart Tweets Table
CREATE TABLE walmart_tweets(
    tweet_id BIGINT(20),
    tweet_text TEXT,
    created_at TEXT,
    tweet TEXT,
    favourite_count BIGINT(20),
    retweet_count BIGINT(20),
    user_id BIGINT(20),
    PRIMARY KEY  (tweet_id)
);

Walmart Tweet URL table
CREATE TABLE walmart_tweet_url(
    tweet_id BIGINT(20),
    tweet_url TEXT,
);


Walmart tweet mention table
CREATE TABLE walmart_tweet_mentions(
    tweet_id BIGINT(20),
    source_user TEXT,
);

Walmart tweet tag table
CREATE TABLE walmart_tweet_tag(
    tweet_id BIGINT(20),
    tags TEXT,
);

Target Tweets Table
CREATE TABLE target_tweets(
    tweet_id BIGINT(20),
    tweet_text TEXT,
    created_at TEXT,
    tweet TEXT,
    favourite_count BIGINT(20),
    retweet_count BIGINT(20),
    user_id BIGINT(20),
    PRIMARY KEY  (tweet_id)

);

Target Tweet URL table
CREATE TABLE target_tweet_url(
    tweet_id BIGINT(20),
    tweet_url TEXT,
);


Target tweet mention table
CREATE TABLE target_tweet_mentions(
    tweet_id BIGINT(20),
    source_user TEXT,
);

Target tweet tag table
CREATE TABLE target_tweet_tag(
    tweet_id BIGINT(20),
    tags TEXT,
);

SamsClub Tweet Table
CREATE TABLE samsclub_tweets(
    tweet_id BIGINT(20),
    tweet_text TEXT,
    created_at TEXT,
    tweet TEXT,
    favourite_count BIGINT(20),
    retweet_count BIGINT(20),
    user_id BIGINT(20),
    PRIMARY KEY  (tweet_id)
);

SamsClub Tweet url table
CREATE TABLE samsclub_tweet_url(
    tweet_id BIGINT(20),
    tweet_url TEXT,
);

SamsClub tweet mention table
CREATE TABLE samsclub_tweet_mentions(
    tweet_id BIGINT(20),
    source_user TEXT,
);

SamsClub tweet tag table
CREATE TABLE samsclub_tweet_tag(
    tweet_id BIGINT(20),
    tags TEXT,
);

**2. Queries to Add Constraints to the Tables: **

**Adding Primary Keys:**

ALTER TABLE twitterdeals.walmart_tweets ADD PRIMARY KEY(tweet_id); 
ALTER TABLE target_tweets ADD PRIMARY KEY(tweet_id);
ALTER TABLE samsclub_tweets ADD PRIMARY KEY(tweet_id);

**Adding Foreign Keys:**

ALTER TABLE twitterdeals.walmart_tweets ADD CONSTRAINT user_id_fk FOREIGN KEY (user_id) REFERENCES twitterdeals.twitter_users(user_id) ON DELETE NO ACTION ON UPDATE NO ACTION; 

ALTER TABLE twitterdeals.walmart_tweet_tag ADD CONSTRAINT tweet_id_fk FOREIGN KEY (tweet_id) REFERENCES twitterdeals.walmart_tweets (tweet_id) ON DELETE NO ACTION ON UPDATE NO ACTION;

ALTER TABLE twitterdeals.walmart_tweet_mentions ADD CONSTRAINT tweet_id_fk2 FOREIGN KEY (tweet_id) REFERENCES twitterdeals.walmart_tweets (tweet_id) ON DELETE NO ACTION ON UPDATE NO ACTION;

ALTER TABLE twitterdeals.walmart_tweet_url ADD CONSTRAINT tweet_id_fk3 FOREIGN KEY (tweet_id) REFERENCES twitterdeals.walmart_tweets (tweet_id) ON DELETE NO ACTION ON UPDATE NO ACTION;

ALTER TABLE target_tweets ADD CONSTRAINT user_id_fk2 FOREIGN KEY (user_id) REFERENCES twitter_users(user_id) ON DELETE NO ACTION ON UPDATE NO ACTION;

ALTER TABLE target_tweet_tag ADD CONSTRAINT tweet_id_fk4 FOREIGN KEY (tweet_id) REFERENCES target_tweets (tweet_id) ON DELETE NO ACTION ON UPDATE NO ACTION;        

ALTER TABLE target_tweet_mentions ADD CONSTRAINT tweet_id_fk5 FOREIGN KEY (tweet_id) REFERENCES target_tweets (tweet_id) ON DELETE NO ACTION ON UPDATE NO ACTION;   

ALTER TABLE target_tweet_url ADD CONSTRAINT tweet_id_fk6 FOREIGN KEY (tweet_id) REFERENCES target_tweets (tweet_id) ON DELETE NO ACTION ON UPDATE NO ACTION;

ALTER TABLE samsclub_tweets ADD CONSTRAINT user_id_fk3 FOREIGN KEY (user_id) REFERENCES twitter_users(user_id) ON DELETE NO ACTION ON UPDATE NO ACTION;

ALTER TABLE samsclub_tweet_tag ADD CONSTRAINT tweet_id_fk7 FOREIGN KEY (tweet_id) REFERENCES samsclub_tweets (tweet_id) ON DELETE NO ACTION ON UPDATE NO ACTION;

ALTER TABLE samsclub_tweet_mentions ADD CONSTRAINT tweet_id_fk8 FOREIGN KEY (tweet_id) REFERENCES samsclub_tweets (tweet_id) ON DELETE NO ACTION ON UPDATE NO ACTION;

ALTER TABLE samsclub_tweet_url ADD CONSTRAINT tweet_id_fk9 FOREIGN KEY (tweet_id) REFERENCES samsclub_tweets (tweet_id) ON DELETE NO ACTION ON UPDATE NO ACTION;


**Use Cases with SQL Queries and Relational Algebra Depiction:**

**1. Use Case:** Get all the users who have tweeted regarding Walmart Deals
Description: View all the Twitter users who have tweeted regarding Walmart Black Friday Deals
Actor: Walmart Admin
Precondition: The user must have a Twitter account
Steps:
Actor action: Search for tags such as #BlackFriday #Walmart
System Responses: Retrieves all the tweets that match the tags used. Get the user name who has tweeted the tweets. The use case ends.
Post Condition: Users retrieved successfully.
Alternate Path: Searches with wrong hashtags and keywords
Error: Gets incorrect and irrelevant tweets.

**Relational Algebra Equation:**
σt.user_id=u.user_id(Πt.tweet_id, t.user_id, u.user_name) (walmart_tweets t, twitter_users u))

**SQL Query:**
SELECT t.tweet_id, t.user_id, u.user_name
FROM Walmart_tweets t, twitter_users u
WHERE t.user_id = u.user_id;

**2. Use Case:** Get all the URLs mentioned in Walmart Deals tweets
Description: View all the URLs mentioned in the tweets regarding Walmart Black Friday Deals
Actor: User
Precondition: The tweet must have a URL in the tweet.
Steps:
Actor action: Search for tags such as #Walmart #DealsForDays.
System Responses: Retrieves all the tweets and gets the URL mentioned in the tweets. Use case ends.
Post Condition: URLs for Walmart deals viewed successfully.
Alternate Path: Gets no tweet with URLs due to wrong search of keywords
Error: Gets no URLs mentioned in tweets.

**Relational Algebra Equation:**
(Πtweet_url (walmart_tweets))

**SQL Query:**
SELECT tweet_url
FROM Walmart_tweet_url;


**3. Use Case:** Get all the text in tweets that mentioned about Walmart Black Friday Deals 
Description: View all the tweets tweeted by various users regarding Walmart Black Friday Deals
Actor: User
Precondition: There must be a tweets thread regarding Black Friday Deals in Walmart.
Steps:
Actor action: Search for tags such as #Walmart #DealsForDays #BlackFriday.
System Responses: Retrieves all the tweets that various users have made regarding the keywords entered. Use case ends.
Post Condition: Tweets returned with respect to the keywords.
Alternate Path: Gets no tweets.
Error: Get no tweets for the given hashtags.

**Relational Algebra Equation:**
𝜎t.user_id=u.user_id(Π.user_name, t.tweet_text (walmart_tweets t, twitter_users u))

**SQL Query:**
SELECT u.user_name, t.tweet_text
FROM twitter_users u, walmart_tweets t
WHERE t.user_id = u.user_id;

**4. Use Case:** Get the top 10 tweets regarding Black Friday sales in Walmart
Description: View all the recently tweeted tweets regarding Walmart’s Deals.
Precondition: Twitter users must be tweeting about the deals in Walmart.
Steps:
Actor action: Search for Walmart.
System Responses: Retrieves all the tweets made for the keywords. Use case ends.
Post Condition: Latest tweets regarding the deals are returned.
Alternate Path: Gets tweets that were made one day ago.
Error: Get no tweets that were made within the present day.

**	Relational Algebra does not support LIMIT**


**SQL Query:**
SELECT tweet_text, created_at
FROM walmart_tweets
ORDER BY created_at DESC
LIMIT 10;

**5. Use Case:** Tweet regarding the deals given for laptops.
Description: The user tweets regarding the deals offered by Walmart for Laptops
Precondition: Must have a Twitter user account.
Steps:
Actor action: Write a tweet regarding Walmart deals with hashtags related to Walmart .
System Responses: Posts the tweet in the user’s timeline.
Post Condition: When another users searches with the keywords, this tweet can be viewed.
Alternate Path: Not adding hashtags and keywords.
Error: Will not appear when another user searches with keywords.

**SQL Query:**

INSERT INTO Walmart_tweets (tweet_id, tweet_text, favorite_count, retweet_count, tweet, user_id)
VALUES (458796966949029616, “Good Phone Deals in Walmart for this Thanks Giving #DealsForDays.😉”, “2022-11-11 00:47:26+00:00”, 0, 0, “Walmart#DealsForDays”, 1579936718937006082);


INSERT INTO twitter_users (tweet_id, user_id, user_name, follower_count,
friend_count, user_profile_image, user_created_at)
VALUES (458796966949029616, 1579936718937006082, “Amretasre_RT_15”, 0, 0, “https://pbs.twimg.com/profile_images/1579936822460833798/HQg--2xw_400x400.jpg”,  2022-10-11 00:47:26+00:00 )

** 6. Use case:** View the products having discounts in Sam’s Club 
Description: The system must be able to display all products having having discounts in Sam’s Club
Actors: User
Precondition: Every tweet should be unique
Steps:
Actor Action: User searches for the discounts
Post Condition: System displays all the products having discounts offered by Sam’s club
Alternate Path: There are no discounts offered by Sam’s club.
Error: There are no discounts

**Relational Algebra Equation:**
σt.user_id=u.user_id(Π.user_name, t.tweet_text (samsclub_tweets t, twitter_users u))

**SQL QUERY**
SELECT 
    u.user_name, t.tweet_text
FROM
    twitterdeals.twitter_users u,
    twitterdeals.samsclub_tweets t
WHERE
    t.user_id = u.user_id;


**7. Use Case:** Display hashtags for Deals in Target 
Description: Displaying all the hashtags for the deals in the Target
Actors: User
Precondition: The tweet must have a hashtag
Steps:
Actor Action: User searches for the hashtags of the deals in the Target.
Post Condition: The system displays all the hashtags of deals in Target.
Alternate Path: There are no hashtags for the deals in Target
Error: There are no deals

**Relational Algebra Equation:**
(Πtags (target_tweets))

**SQL QUERY:**
SELECT 
    tags
FROM
    twitterdeals.target_tweet_tag;

 **8.	Use Case:** List all users having followers more than 10k
Description: Displays the list of users having more than 10k followers
Action: User
Precondition: The users should have more than 10k followers
Steps:
Actor action: The user searched for the list of users having more than 10k followers
System response: List of users having 10k followers is displayed
Post condition: System displays the list of users
Alternate path: Gets no list
Error: No user has more than 10k followers

**Relational Algebra Equation:**
σ follower_count>10000 (∏COUNT(user_id)(twitter_users))

**SQL QUERY**
SELECT 
    COUNT(user_id)
FROM
    twitterdeals.twitter_users
WHERE
    follower_count > 10000;


**9. Use Case:** View all the URLs of the tweets
Description: Displays the URLs of all the tweets in the database
Actor: User
Precondition: There should be URLs in tweets.
Steps:
Action actor: User searched for all the URLs of the tweets
System response: list of URLs would be displayed
Post condition: System displays the list of URLs
Alternate path: Tweets not present
Error: No URL found

**Relational Algebra Equation: **
 (∏w.tweet_url,t.tweet_url,s.tweet_url(walmart_tweets w, target_tweets t, samsclub_tweets s))

**SQL Query**
SELECT DISTINCT
    w.tweet_url, t.tweet_url, s.tweet_url
FROM
    twitterdeals.walmart_tweet_url w,
    twitterdeals.target_tweet_url t,
    twitterdeals.samsclub_tweet_url s;

**10. Use Case:** Show the URL of the tweet having BlackFriday
Description: Displays the URL of the tweet having BlackFriday
Actor: User
Precondition: Tweet URL must have a BlackFriday
Steps:
Action actor: User searches for the URL of the tweet having BlackFriday
System response: URL of the tweet having BlackFriday would be displayed
Post condition: System displays the URL
Alternate path: Tweet does not have BlackFriday
Error: Nor URL found

**Relational Algebra Equation:**
σ(w.tweet_url LIKE ‘%BlackFriday%’) OR (t.tweet_url LIKE ‘%BlackFriday%’) OR (s.tweet_url LIKE ‘%BlackFriday%’)( (∏w.tweet_url,t.tweet_url,s.tweet_url(walmart_tweets w,
target_tweets t, samsclub_tweets s)))

**SQL Query:**
SELECT distinct w.tweet_url, t.tweet_url, s.tweet_url
FROM walmart_tweet_url w, target_tweet_url t,samsclub_tweet_url s
WHERE w.tweet_url LIKE '%BlackFriday%' OR t.tweet_url LIKE '%BlackFriday%' OR  s.tweet_url LIKE '%BlackFriday%' ;

**11. Use Case:** Count total number of users having retweets more than 10 for Target
Description: Displays the number users with retweets more than 10
Action: User
Precondition: The retweet should have more than 10
Steps:
Actor action: The user searches for the list of all the retweets more than 10 
System response: The number of users would be displayed
Post condition: System displays the list of all the tweets
Alternate path: There were no retweets less than 10
Error: There were no tweets

**Relational Algebra Expressions -** 
𝛔retweet_count>10(ΠCOUNT(user_id) (twitterdeals.target_tweets))


**SQL Query:**
SELECT COUNT(user_id)
FROM twitterdeals.target_tweets
WHERE retweet_count > 10;

**12.Use Case:** View all the users mentioned in tweets related to Samsclub
Description: Displays the list of users who are mentioned in tweets related to Walmart
Actor: User
Precondition: Tweet must have the name of the user 
Steps:
Actor action: The user searches for the list of all the users who have been tagged in the tweets related to Walmart
System response: The list of users would be displayed
Post condition: The system displays the list of users tagged
Alternate path: There were no users tagged in the tweets related to Walmart
Error: There were no

**Relational Algebra Expressions:** 
ΠDISTINCT source_user  (twitterdeals.target_tweets))

**SQL Query:**
SELECT DISTINCT source_user 
FROM twitterdeals.samsclub_tweet_mentions;

**13. Use Case:** Display a list of tweets in Target that have likes more than 50
Description: Tweets having likes more than 50
Action: User
Precondition: The tweet should have more than 50 likes
Steps:
Actor action: The user searches for the list of all the tweets that have more than 50 likes
System response: The list of tweets would be displayed
Post condition: System displays the list of all the tweets
Alternate path: There were no tweets having more than 50 likes
Error: There were no tweets

**Relational Algebra:** 
𝛔favorite_count > 50 (Πtweet_text (twitterdeals.walmart_tweets))

**SQL Query:**
SELECT tweet_text 
FROM twitterdeals.walmart_tweets
WHERE favorite_count > 50;


**14. UseCase:** View the tweet related to the #Deals #Target by user having user_id '4161180381'
Description: Displays the details of the user having user_id 12345678 related to the tweet #Deals
Actor: User
Precondition: The user should have tweeted related to #Deals
Steps:
Actor action: User searches for the details of the user having user_id 12345678 related to #Deals
System response: Details of the user would be displayed
Post condition: System displays the details of the user
Alternate path: User having user_id  '4161180381' has not tweeted anything related to the tweet #DealsError: No details found

**Relational Algebra:** 
𝛔 t.tweet_id=tw.tweet_id and t.user_id = 4161180381(Πt.tweet_text, t.created_at, tw.tweet_url ( twitterdeals.target_tweets t, twitterdeals.target_tweet_url tw)


**SQL Query:** 
SELECT t.tweet_text, t.created_at, tw.tweet_url
FROM twitterdeals.target_tweets t, twitterdeals.target_tweet_url tw
WHERE t.tweet_id=tw.tweet_id and t.user_id = 4161180381;

**15. Use case:**  View all the tweets posted last 24 hours on SamsClub
Description: Displays the tweets posted on SamsClub in the last 24 hours
Actor: User
Precondition: SamsClub should have at least one tweet in the past 24 hours
Steps:
Actor action: User searches for the tweets posted on SamsClub in the last 24 hours
System response: Displays the list of tweets posted on SamsClub in the past 24 hours
Post condition: System displays the tweets posted
Alternate path: SamsClub did not post any tweet in the last 24 hours
Error: No tweet found

**Relational Algebra:** 
𝛔 tweet_date = CURDATE()(Π tweet_text(twitterdeals.samsclub_tweets)

 **SQL query:**
SELECT tweet_text
FROM twitterdeals.samsclub_tweets
where tweet_date = CURDATE();

**16.Use Case:** Count the number of users tweeted on the date 10 Nov 2022 for all 3 merchants
Description: Displays the count of users who tweeted on 10 Nov 2022
Action: User
Precondition: The users should have tweeted in 10 Nov 2022
Steps:
Actor action: The user searches for the users who tweeted on 10 Nov 2022
System response: The count of users would be displayed
Post condition: System displays the count of users
 Alternate path:  Gets no count
Error: No tweets on 10 Nov 2022

**Relational Algebra:** 
𝛔 t.created_at=CURDATE() AND w.created_at=CURDATE() AND s.created_at=CURDATE()(Π COUNT(t.user_id), COUNT(w.user_id), COUNT(s.user_id)(target_tweets t, walmart_tweets w,samsclub_tweets s)

**SQL QUERY:**
SELECT COUNT(t.user_id) as table1Count, COUNT(w.user_id) as table2Count, COUNT(s.user_id) as table3Count
FROM target_tweets t, walmart_tweets w,samsclub_tweets s
WHERE t.created_at=CURDATE() AND w.created_at=CURDATE() AND s.created_at=CURDATE();

**17.Use Case:**	View all the tweets related to SamsClub and Target
Description: Displays all the tweets related to SamsClub and Target
Actor: User
Precondition: There should be at least one tweet related to Walmart and one tweet related to Target
Steps:
Action actor: User searched for all the tweets related to SamsClub and Target
System response: System would show the tweets related to SamsClub and Target
Post condition: List of the tweets is displayed
Alternate path: There are no tweets related to SamsClub and Target
Error: Tweets not found

**Relational Algebra:**
(Π * (twitterdeals.samsclub_tweets)) ∪ (Π * (twitterdeals.target_tweets))

**SQL Query:** 
SELECT * FROM twitterdeals.samsclub_tweets
UNION
SELECT * FROM twitterdeals.target_tweets;


**18. UseCase:**  Display all the tweets from 5 November 2022 to 10 November 2022 for SamsClub
Description: The user must be able to view all the tweets that he made from  5 November 2022 to 10 November 2022 
Actors: User
Precondition: The tweets must be saved in the database according to the date.
Steps:
Actor Action: User searches for the tweets that was made on  5 November 2022 to 10 November 2022 
Post Condition: System displays all the tweets posted on  5 November 2022 to 10 November 2022 to the date.
Alternate Path: There were no tweets by user from  5 November 2022 to 10 November 2022 
Error: There are no tweets.

**Relational Algebra:** 
𝛔tweet_date between 2022-11-09 and 2022-11-11(Π(twitterdeals.samsclub_tweets)

**SQl Query:**
SELECT * 
FROM twitterdeals.samsclub_tweets
WHERE tweet_date between 2022-11-09 and 2022-11-11;

**19. Use Case:** Tweet regarding the discounts and deals on groceries in SamsClub.
Description: The user tweets regarding the discounts offered by SamsClub.for groceries
Precondition: Must have a Twitter user account.
Steps:
Actor action: Write a tweet regarding Walmart deals with hashtags related to SamsClub.
System Responses: Posts the tweet in the user’s timeline.
Post Condition: When another users searches with the keywords, this tweet can be viewed.
Alternate Path: Not adding hashtags and keywords.
Error: Will not appear when another user searches with keywords.

**SQL Query:**
INSERT INTO SamsClub_tweets (tweet_id, tweet_text, favorite_count, retweet_count, tweet, user_id)
VALUES (12312239669900775349, “Fresh Fruits and Vegetables Special Thanksgiving Discount on min 5lbs”, #Discount.”, “2022-11-12 00:24:41+00:00”, 0, 0, “Target#20%OFF#Discount#Deals”, 2313458937445567);


INSERT INTO twitter_users (tweet_id, user_id, user_name, follower_count,
friend_count, user_profile_image, user_created_at)
VALUES (12312239669900775349, 2313458937445567, “RitaSamsClub”, 0, 0, “https://pbs.twimg.com/profile_images/2313458937445567/HQg--2xw_400x400.jpg”,  2012-10-07 00:22:56+00:00 )


**20. Use Case:** View all the tweets tags related to SamsClub on 6 Nov 2022.
Description: Displays all the tweets tags related to  SamsClub on 6 November 2022
Actor: User
Precondition: There should be at least one tweet tags related to SamsClub
Steps:
Action actor: User searched for all the tweets tags related to  SamsClub
System response: System would show the tweet tags related to  SamsClub  posted on 6 Nov 2022.
Post condition: List of the tweets tags is displayed
Alternate path: There are no tweets related to  SamsClub
Error: Tweets not found

**Relational Algebra:** 
𝛔 st.tweet_id = s.tweet_id AND s.tweet_date = 2022-11-06(Π st.tags, st.tweet_id(twitterdeals.samsclub_tweet_tag st, 
    twitterdeals.samsclub_tweets s)


**SQL Query-** 
SELECT st.tags, st.tweet_id
FROM
    twitterdeals.samsclub_tweet_tag st, 
    twitterdeals.samsclub_tweets s
WHERE
    st.tweet_id = s.tweet_id AND s.tweet_date = 2022-11-06;
