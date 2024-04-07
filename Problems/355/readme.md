# [355. Design Twitter](https://leetcode.com/problems/design-twitter/)

Design a simplified version of Twitter where users can post tweets, follow/unfollow another user, and is able to see the `10` most recent tweets in the user's news feed.

Implement the `Twitter` class:

- `Twitter()` Initializes your twitter object.
- `void postTweet(int userId, int tweetId)` Composes a new tweet with ID `tweetId` by the user `userId`. Each call to this function will be made with a unique `tweetId`.
- `List<Integer> getNewsFeed(int userId)` Retrieves the `10` most recent tweet IDs in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user themself. Tweets must be **ordered from most recent to least recent**.
- `void follow(int followerId, int followeeId)` The user with ID `followerId` started following the user with ID `followeeId`.
- `void unfollow(int followerId, int followeeId)` The user with ID `followerId` started unfollowing the user with ID `followeeId`.

**Example 1:**

**Input**
["Twitter", "postTweet", "getNewsFeed", "follow", "postTweet", "getNewsFeed", "unfollow", "getNewsFeed"]
[[], [1, 5], [1], [1, 2], [2, 6], [1], [1, 2], [1]]
**Output**
[null, null, [5], null, null, [6, 5], null, [5]]

**Explanation**
Twitter twitter = new Twitter();
twitter.postTweet(1, 5); // User 1 posts a new tweet (id = 5).
twitter.getNewsFeed(1); // User 1's news feed should return a list with 1 tweet id -> [5]. return [5]
twitter.follow(1, 2); // User 1 follows user 2.
twitter.postTweet(2, 6); // User 2 posts a new tweet (id = 6).
twitter.getNewsFeed(1); // User 1's news feed should return a list with 2 tweet ids -> [6, 5]. Tweet id 6 should precede tweet id 5 because it is posted after tweet id 5.
twitter.unfollow(1, 2); // User 1 unfollows user 2.
twitter.getNewsFeed(1); // User 1's news feed should return a list with 1 tweet id -> [5], since user 1 is no longer following user 2.

## **Constraints:**

- `1 <= userId, followerId, followeeId <= 500`
- `0 <= tweetId <= 104`
- All the tweets have **unique** IDs.
- At most `3 * 104` calls will be made to `postTweet`, `getNewsFeed`, `follow`, and `unfollow`.

## Solution

To implement the simplified version of Twitter, we can use the following data structures:

- A dictionary to store the list of tweets for each user.
- A dictionary to store the set of followees for each user.
- A global timestamp to keep track of the order of tweets.

Here's how we can implement each method:

1. **`__init__`:** Initialize the dictionaries and the timestamp.
2. **`postTweet`:** Add the tweet to the user's list of tweets along with the current timestamp. Increment the timestamp.
3. **`getNewsFeed`:** Retrieve the 10 most recent tweets from the user and their followees. This can be done by merging the lists of tweets and selecting the 10 most recent ones.
4. **`follow`:** Add the followee to the user's set of followees.
5. **`unfollow`:** Remove the followee from the user's set of followees.

```python
class Twitter:
    def __init__(self):
        self.tweets = {}
        self.followees = {}
        self.timestamp = 0

    def postTweet(self, userId: int, tweetId: int) -> None:
        if userId not in self.tweets:
            self.tweets[userId] = []
        self.tweets[userId].append((self.timestamp, tweetId))
        self.timestamp += 1

    def getNewsFeed(self, userId: int) -> list[int]:
        feed = []
        if userId in self.tweets:
            feed.extend(self.tweets[userId][-10:])
        if userId in self.followees:
            for followee in self.followees[userId]:
                if followee in self.tweets:
                    feed.extend(self.tweets[followee][-10:])
        feed.sort(reverse=True)
        return [tweetId for _, tweetId in feed[:10]]

    def follow(self, followerId: int, followeeId: int) -> None:
        if followerId not in self.followees:
            self.followees[followerId] = set()
        self.followees[followerId].add(followeeId)

    def unfollow(self, followerId: int, followeeId: int) -> None:
        if followerId in self.followees and followeeId in self.followees[followerId]:
            self.followees[followerId].remove(followeeId)

# Example usage
twitter = Twitter()
twitter.postTweet(1, 5)
print(twitter.getNewsFeed(1))  # Output: [5]
twitter.follow(1, 2)
twitter.postTweet(2, 6)
print(twitter.getNewsFeed(1))  # Output: [6, 5]
twitter.unfollow(1, 2)
print(twitter.getNewsFeed(1))  # Output: [5]

```

## Thoughts

Pretty complicated with a lot of edge cases, needs review many times

### Time Complexity

- **`postTweet`:** O(1)
- **`getNewsFeed`:** O(m log m), where m is the total number of tweets in the user's feed (including their own and their followees'). The sorting step dominates the time complexity.
- **`follow`:** O(1)
- **`unfollow`:** O(1)

### Space Complexity

- O(n + m), where n is the number of users and m is the total number of tweets. The space complexity is determined by the size of the `tweets` and `followees` dictionaries.
