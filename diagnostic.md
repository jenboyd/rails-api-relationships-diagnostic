# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

```sh
Joining tables is valuable because it allows you to keep data consistent across multiple
tables by linking them.
```

1.  Provide a database table structure and explain the Entity Relationship that
describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
(Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
`Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
join table with references to `Movies` and `Profiles`.

```sh
Profiles have `given_name`, `surname` and `email`
Movies have `title`, `release_date`
Favorites have movie_id and profile_id
```

1.  For the above example, what needs to be added to the Model files?

```rb
class Profile < ActiveRecord::Base
  has_many: :Movies, through: :Favorites
end
```

```rb
class Movie < ActiveRecord::Base
  belongs_to: :Profiles, through: :Favorites
end
```

```rb
class Favorite < ActiveRecord::Base
  has_many: :Movies
  has_many: :Profiles
end
```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

```sh
  Profile {
    "id" : 1,
    "favorites" : {
      "movies" : {
        ["title" : "", "release_date" : ""],
        ["title" : "", "release_date" : ""],
        ["title" : "", "release_date" : ""],
      }
      }
    }
  }
```

```rb
class ProfileSerializer < ActiveModel::Serializer
end
```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

```sh
bundle exec rails g scaffold Favorites Movie: references Profile: References
```

1.  What is `Dependent: Destroy` and where/why would we use it?

```sh
We put `Dependent: Destroy` in locations where we want the data to be destroyed
if certain relationships between data are destroyed.
```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

```sh
In the case of a simlple blog, users have a many posts.

In a more complex blog like Pinterest, users have many posts, but posts also
have many users. Users also have favorites with many posts and Boards with many posts.
```
