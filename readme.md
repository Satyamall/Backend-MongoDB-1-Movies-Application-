
# MongoDB Queries for Movies Application

```js
mongoimport --db movies --collection movies --file movies.json --port 27017 --jsonArray
```
**Output-**
2022-02-11T11:48:07.143+0530    connected to: mongodb://localhost:27017/
2022-02-11T11:48:07.151+0530    Failed: cannot decode array into a primitive.D
2022-02-11T11:48:07.151+0530    0 document(s) imported successfully. 0 document(s) failed to import.

```js
 show dbs
 ```
admin     41 kB
airbnb  54.7 MB
config   111 kB
local   73.7 kB
masai    274 kB
movies  65.5 kB

```js
 use movies
 ```
switched to db movies
movies> show collections
movies

#  1. Find all movies which are equal to movie_name.
```js
db.movies.find({movie_name: "Bitter Sweetheart"})
```
**Output-**
[
  {
    _id: ObjectId("6206015339c97eef66aa8e92"),
    id: 25,
    movie_name: 'Bitter Sweetheart',
    movie_genre: 'Comedy|Drama',
    'production_year ': 2006,
    'budget ': 11823
  }
]

```js
db.movies.find({movie_name: {$eq:"Bitter Sweetheart"}})
```
[
  {
    _id: ObjectId("6206015339c97eef66aa8e92"),
    id: 25,
    movie_name: 'Bitter Sweetheart',
    movie_genre: 'Comedy|Drama',
    'production_year ': 2006,
    'budget ': 11823
  }
]

**Below Picture for above querry**
![Screenshot (224)](https://user-images.githubusercontent.com/80479635/153556090-087427a8-fef2-4ee6-adc2-193489f3183e.png)



# 2. find all movies which are not equal to movie_name.
```js
db.movies.find({movie_name: {$ne:"Bitter Sweetheart"}}).count()
```
**Output-** 499
```js
db.movies.find({movie_name: {$ne:"Bitter Sweetheart"}})
```
**Output-**
[
  {
    _id: ObjectId("6206015339c97eef66aa8e80"),
    id: 6,
    movie_name: 'The Outsider',
    movie_genre: 'Action|Crime|Drama',
    'production_year ': 2001,
    'budget ': 18070
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e81"),
    id: 9,
    movie_name: 'Shiloh',
    movie_genre: 'Children|Drama',
    'production_year ': 2005,
    'budget ': 10092
  },
  ...................
  ...............
  .....
  .....
**Below Picture for above querry**
![Screenshot (225)](https://user-images.githubusercontent.com/80479635/153556120-fa5d578a-c41d-4fd4-aeba-608d4b73f566.png)


# 3. find all movies greater than and greater than equal to a budget
```js
db.movies.find({'budget ': {$gte: 16150}}).count()
```
**Output-** 171

```js
db.movies.find({'budget ': {$gte: 16150}})
```
**Output-**
[
  {
    _id: ObjectId("6206015339c97eef66aa8e80"),
    id: 6,
    movie_name: 'The Outsider',
    movie_genre: 'Action|Crime|Drama',
    'production_year ': 2001,
    'budget ': 18070
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e82"),
    id: 10,
    movie_name: 'That Day, on the Beach (Hai tan de yi tian)',
    movie_genre: 'Drama',
    'production_year ': 1992,
    'budget ': 18114
  },
   ...................
  ...............
  .....
  .....
**Below Picture for above querry**
![Screenshot (226)](https://user-images.githubusercontent.com/80479635/153556149-cbe547c4-ec1b-4056-84a7-fa1d02fb0fde.png)



# 4. find all movies less than and less than equal to a budget.
```js
db.movies.find({'budget ': {$lte: 16150}}).count()
```
**Output-** 330

```js
db.movies.find({'budget ': {$lte: 16150}})
```
**Output-**
[
  {
    _id: ObjectId("6206015339c97eef66aa8e81"),
    id: 9,
    movie_name: 'Shiloh',
    movie_genre: 'Children|Drama',
    'production_year ': 2005,
    'budget ': 10092
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e84"),
    id: 12,
    movie_name: 'The Perfect World of Kai',
    movie_genre: 'Animation|Drama',
    'production_year ': 2017,
    'budget ': 9863
  },
  ...................
  ...............
  .....
  .....
**Below Picture for above querry**
![Screenshot (227)](https://user-images.githubusercontent.com/80479635/153556175-c0816187-b7fa-49cf-b08d-8a3a91f6c0a4.png)



# 5. find all movies that are produced after 2000 with budget greater than 10000.
```js
db.movies.find({'production_year ': {$gt: 2000},'budget ': {$gt: 10000 }}).count()
```
**Output-** 294

```js
db.movies.find({'production_year ': {$gt: 2000},'budget ': {$gt: 10000 }})
```
**Output-**
[
  {
    _id: ObjectId("6206015339c97eef66aa8e80"),
    id: 6,
    movie_name: 'The Outsider',
    movie_genre: 'Action|Crime|Drama',
    'production_year ': 2001,
    'budget ': 18070
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e81"),
    id: 9,
    movie_name: 'Shiloh',
    movie_genre: 'Children|Drama',
    'production_year ': 2005,
    'budget ': 10092
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e85"),
    id: 13,
    movie_name: 'A Cry in the Wild',
    movie_genre: 'Action|Adventure|Thriller',
    'production_year ': 2020,
    'budget ': 16867
  },
  ...................
  ...............
  .....
  .....
**Below Picture for above querry**
![Screenshot (228)](https://user-images.githubusercontent.com/80479635/153556203-07b9f242-4179-462e-8dd4-d87b32625140.png)



# 6. find all movies that are produced after 2000 or budget greater than 10000.
```js
db.movies.find({$or:[{'production_year ': {$gt: 2000}},{'budget ': {$gt: 10000 }}]}).count()
```
**Output-** 485

```js
db.movies.find({$or:[{'production_year ': {$gt: 2000}},{'budget ': {$gt: 10000 }}]})
```
**Output-**
[
  {
    _id: ObjectId("6206015339c97eef66aa8e80"),
    id: 6,
    movie_name: 'The Outsider',
    movie_genre: 'Action|Crime|Drama',
    'production_year ': 2001,
    'budget ': 18070
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e81"),
    id: 9,
    movie_name: 'Shiloh',
    movie_genre: 'Children|Drama',
    'production_year ': 2005,
    'budget ': 10092
  },
  {
 ...................
  ...............
  .....
  .....
**Below Picture for above querry**
![Screenshot (229)](https://user-images.githubusercontent.com/80479635/153556229-9c77b294-c241-45e2-9a9e-d03fdbbc2607.png)


# 7. find all movies that are neither produced after 2000 nor with budget greater than 10000.
```js
db.movies.find({$nor:[{'production_year ': {$gt: 2000}},{'budget ': {$gt: 10000 }}]}).count()
```
**Output-** 15

```js
db.movies.find({$nor:[{'production_year ': {$gt: 2000}},{'budget ': {$gt: 10000 }}]})
```
**Output-**
[
  {
    _id: ObjectId("6206015339c97eef66aa8ee5"),
    id: 102,
    movie_name: 'Days Of Darkness',
    movie_genre: 'Horror',
    'production_year ': 1996,
    'budget ': 9516
  },
  {
    _id: ObjectId("6206015339c97eef66aa8f06"),
    id: 128,
    movie_name: 'Believer, The',
    movie_genre: 'Drama',
    'production_year ': 1996,
    'budget ': 9087
  },
  {
    _id: ObjectId("6206015339c97eef66aa8f0c"),
    id: 147,
    movie_name: 'Soldiers of Fortune',
    movie_genre: 'Action|Adventure',
    'production_year ': 1997,
    'budget ': 9621
  },
  {
   ...................
  ...............
  .....
  .....
**Below Picture for above querry**
![Screenshot (230)](https://user-images.githubusercontent.com/80479635/153556263-bb8aa172-c08d-48a6-a358-c17316f3954a.png)



# 8. find all movies that are not produced in 2000 or they do not have budget of 10000.
```js
db.movies.find({$or:[{'production_year ': {$ne: 2000}},{'budget ': {$ne: 10000 }}]}).count()
```
**Output-** 500

```js
db.movies.find({$or:[{'production_year ': {$ne: 2000}},{'budget ': {$ne: 10000 }}]})
```
**Output-**
[
  {
    _id: ObjectId("6206015339c97eef66aa8e80"),
    id: 6,
    movie_name: 'The Outsider',
    movie_genre: 'Action|Crime|Drama',
    'production_year ': 2001,
    'budget ': 18070
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e81"),
    id: 9,
    movie_name: 'Shiloh',
    movie_genre: 'Children|Drama',
    'production_year ': 2005,
    'budget ': 10092
  },
  {
  ...................
  ...............
  .....
  .....
**Below Picture for above querry**
![Screenshot (231)](https://user-images.githubusercontent.com/80479635/153556285-e873f316-7a75-4d8e-93ba-408414fae644.png)



# 9. find all movies that were produced from 2000 to 2010.
```js
db.movies.find({'production_year ': {$gte: 2000, $lte: 2010 }}).count()
```
**Output-** 168

```js
db.movies.find({'production_year ': {$gte: 2000, $lte: 2010 }})
```
**Output-** 
[
  {
    _id: ObjectId("6206015339c97eef66aa8e80"),
    id: 6,
    movie_name: 'The Outsider',
    movie_genre: 'Action|Crime|Drama',
    'production_year ': 2001,
    'budget ': 18070
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e81"),
    id: 9,
    movie_name: 'Shiloh',
    movie_genre: 'Children|Drama',
    'production_year ': 2005,
    'budget ': 10092
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e8c"),
    id: 20,
    movie_name: 'Lassie',
    movie_genre: 'Adventure|Children',
    'production_year ': 2006,
    'budget ': 14098
  },
  {
  ...................
  ...............
  .....
  .....
**Below Picture for above querry**
![Screenshot (232)](https://user-images.githubusercontent.com/80479635/153556311-7c3802b2-4f40-45d0-9bd5-252abc4e83bd.png)



# 10. Sort all movies descending based on the production year and if the year is same then alphabetically for their movie_names.
```js
db.movies.find({}).sort({'production_year ': -1,movie_name: 1})
```
**Output-**
[
  {
    _id: ObjectId("6206015339c97eef66aa9069"),
    id: 492,
    movie_name: '5x2',
    movie_genre: 'Drama|Romance',
    'production_year ': 2020,
    'budget ': 11279
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e85"),
    id: 13,
    movie_name: 'A Cry in the Wild',
    movie_genre: 'Action|Adventure|Thriller',
    'production_year ': 2020,
    'budget ': 16867
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e8a"),
    id: 18,
    movie_name: 'Bells of Capistrano',
    movie_genre: 'Western',
    'production_year ': 2020,
    'budget ': 18979
  },
  {
  ...................
  ...............
  .....
  .....
**Below Picture for above querry**
![Screenshot (233)](https://user-images.githubusercontent.com/80479635/153556339-0b8e33ba-59d8-4293-84de-86e50475a281.png)
![Screenshot (234)](https://user-images.githubusercontent.com/80479635/153556345-6fc6fc27-96e3-493d-8b8a-5c86cd865538.png)
![Screenshot (235)](https://user-images.githubusercontent.com/80479635/153556361-1f2beecd-d185-4b33-84b3-79d00070c801.png)


# 11. in query 10 skip the first 10 entries and fetch the next 5.
```js
db.movies.find({}).limit(5).skip(10)
```
**Output-**
[
  {
    _id: ObjectId("6206015339c97eef66aa8e8a"),
    id: 18,
    movie_name: 'Bells of Capistrano',
    movie_genre: 'Western',
    'production_year ': 2020,
    'budget ': 18979
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e8b"),
    id: 19,
    movie_name: 'Quiller Memorandum, The',
    movie_genre: 'Action|Drama|Mystery|Thriller',
    'production_year ': 1999,
    'budget ': 19462
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e8c"),
    id: 20,
    movie_name: 'Lassie',
    movie_genre: 'Adventure|Children',
    'production_year ': 2006,
    'budget ': 14098
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e8d"),
    id: 21,
    movie_name: 'Barbie: A Fashion Fairytale',
    movie_genre: 'Animation|Children',
    'production_year ': 1997,
    'budget ': 18190
  },
  {
    _id: ObjectId("6206015339c97eef66aa8e8e"),
    id: 22,
    movie_name: 'Darkon',
    movie_genre: 'Documentary|Fantasy',
    'production_year ': 2011,
    'budget ': 11547
  }
]

**Below Picture for above querry**
![Screenshot (237)](https://user-images.githubusercontent.com/80479635/153556389-fdeab06d-43ed-4e88-b44c-c14fe1ea9087.png)



# 12. remove movie genre from the first 10 movies in query 10.
```js
db.movies.remove({id: {$lte: 10}},{movie_genre: 1})
```
**Output-**
DeprecationWarning: Collection.remove() is deprecated. Use deleteOne, deleteMany, findOneAndDelete, or bulkWrite.
{ acknowledged: true, deletedCount: 9 }

**Below Picture for above querry**
![Screenshot (238)](https://user-images.githubusercontent.com/80479635/153556415-bc3defe5-9552-4b05-acc9-73c231afe20b.png)


# Final Picture of almost all querries of above.
![Screenshot (239)](https://user-images.githubusercontent.com/80479635/153556444-92a30bc2-12e8-49fd-a0b2-a99deae845af.png)
