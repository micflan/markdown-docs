# API Design for MyApplication

* REST Web Service with 2 base URLs per resource
* HTTP verbs are POST, GET, PUT and DELETE (Create, Read, Update, Delete)

_Example: two (2) resources (/object and /object/XX) and the four (4) HTTP verbs_

## Authorisation

### Attributes

    TO AUTHENTICATE:
    username
    password
    app_key

    RESPONSE:
    token,
    user_id

    EVERY SUBSEQUENT REQUEST MUST CONTAIN:
    access_token: md5(token + app_private_key)
    user_id

#### GET
    /users/auth                        returns user token for future authentication


-----

# Resources

The following is a list of resources supported by the MyApplication API, their attributes and example JSON GET response.

## UserGroups

### Attributes

    Id: [num],
    Name: [string],
    URL Title: [string],
    Image: [string],
    Users: [ { Id } ]

### Response

    [
        {
            "id": 1234,
            "name": "Group 1",
            "url_title": "group_1",
            "image_url": "http://path.to/image.jpg",
            "image_url_https": "https://path.to/image.jpg"
            "users": [
                { 1234 },
                { 1235 },
                { 1236 },
            ]
        }
    ]

#### GET

    /usergroups                         returns list of usergroups
    /usergroups/[id]                    returns a usergroup

-----

## Users

### Attributes

    Id: [num],
    Name: [string],
    First Name: [string],
    Last Name: [string],
    Username: [string],
    Image: [string],
    Is Self: [true|false],
    UserGroup: [
        Id: [num],
        Name: [string],
        URL Title: [string],
        Image: [string]
    ]
    Last Login: [unix time],
    Join Date: [unix time]

### Response

    [
        {
            "id": 1234,
            "name": "Michael Flanagan",
            "first_name": "Michael",
            "last_name": "Flanagan",
            "username": "micflan",
            "image_url": "http://path.to/image.jpg",
            "image_url_https": "https://path.to/image.jpg",
            "is_self": true,
            "usergroup": {
                "id": 1234,
                "name": "Group 1",
                "url_title": "group_1",
                "image_url": "http://path.to/image.jpg",
                "image_url_https": "https://path.to/image.jpg"
            },
            "last_login": 12345678,
            "join_date": 12345678
        }
    ]

#### POST

    /users                              create a user

#### GET

    /users                              returns list of users
    /users/[id]                         returns a user

    OPTIONS
    ?expand=points,achievements,friends,profile

#### PUT

    /users/[id]                         update a user

#### DELETE

    /users/[id]                         delete a user

-----

