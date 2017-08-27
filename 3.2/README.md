# MongoDbRegistrationandLogin
MongoDbRegistrationandLogin

Homework 3.1  MongoDB for .Net Development
Download the students.json file from the Download Handout link and import it into your local Mongo instance with this command:

mongoimport --drop -d school -c students students.json
This dataset holds the same type of data as last week's grade collection, but it's modeled differently. You might want to start by inspecting it in the Mongo shell.

Write a program in the language of your choice that will remove the lowest homework score for each student. Since there is a single document for each student containing an array of scores, you will need to update the scores array and remove the homework.

Remember, just remove a homework score. Don't remove a quiz or an exam!

Hint/spoiler: With the new schema, this problem is a lot harder and that is sort of the point. One way is to find the lowest homework in code and then update the scores array with the low homework pruned.

To confirm you are on the right track, here are some queries to run after you process the data with the correct answer shown:

Let us count the number of students we have:

use school
db.students.count()
The answer will be 200.

Let's see what Tamika Schildgen's record looks like once you have removed the lowest score:

db.students.find( { _id : 137 } ).pretty( )
This should be the output:

{
    "_id" : 137,
    "name" : "Tamika Schildgen",
    "scores" : [
        {
            "type" : "exam",
            "score" : 4.433956226109692
        },
        {
            "type" : "quiz",
            "score" : 65.50313785402548
        },
        {
            "type" : "homework",
            "score" : 89.5950384993947
        }
    ]
}
To verify that you have completed this task correctly, provide the identity (in the form of their _id) of the student with the highest average in the class with following query that uses the aggregation framework. The answer will appear in the _id field of the resulting document.

db.students.aggregate( [
  { '$unwind': '$scores' },
  {
    '$group':
    {
      '_id': '$_id',
      'average': { $avg: '$scores.score' }
    }
  },
  { '$sort': { 'average' : -1 } },
  { '$limit': 1 } ] )

ANS : 13

Homework: Homework 3.2: Making your Blog Accept Posts

In this homework you will be enhancing the blog project to insert entries into the posts collection. After this, the blog will work. It will allow you to add blog posts with a title, content, and tags and have it be added to the posts collection properly.

We have provided the code that creates users and allows you to login (the assignment from last week). To get started, please download the handout and unpack.

The areas where you need to add code are marked with XXX. You need only touch the Post.cs file, the Comments.cs file, and the HomeController.cs file. There are seven locations for you to add code for this problem:

5 in HomeController.cs
1 in Post.cs
1 in Comment.cs
Here is an example of a valid blog post.

> db.posts.find().pretty()
{
        "_id" : ObjectId("54c298ec122ea911588b7970"),
        "Author" : "Craig",
        "Title" : "Frist!!!",
        "Content" : "This is my first post!!!",
        "Tags" : [
                "first",
                "awesome"
        ],
        "CreatedAtUtc" : ISODate("2015-01-23T18:54:36.335Z"),
        "Comments" : [
                {
                        "Author" : "Jack",
                        "Content" : "This is a comment.",
                        "CreatedAtUtc" : ISODate("2015-01-23T18:54:42.005Z")
                }
        ]
}
We are going to validate that this worked properly. We will be checking for the following functionality:

Your blog can accept posts.
Your posts can be tagged.
Your posts can receive comments from others who are logged in.
When you are ready, turn it in using mongoProc.


First of all download this project.

Open it with visual studio 2013 or above version and build your project to find if there is any error.

It will build successfully..

Make sure DLL for MongoDB driver is added in your project otherwise download it with the help of Nugget Package manager.
