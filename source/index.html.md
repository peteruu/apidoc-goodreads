---
title: Goodreads Unofficial Api

language_tabs: # must be one of https://git.io/vQNgJ
- php

search: true
---
# Introduction

Welcome to the Goodreads Unofficial API! You can use our API to access Goodreads content.
In examples we are using Symfony component called [The HttpClient Component](https://symfony.com/doc/current/components/http_client.html).

# Authentication

> Pass your API-key in all API requests as a header. To authorize, use this code:

> Request:

```php
<?php
$api_key = YOURAPIKEY;
$query_parameters = QUERYPARAMETERS;
$host = YOURDOMAIN;

$httpClient = HttpClient::create([
    'headers' => ['X-AUTH-API' => $api_key, 'Referer' => $host],
]);

$response = $httpClient->request('GET', 'https://affwebgen.com/api', ['query' => $query_parameters,]);

?>
```


> Make sure to replace `YOURAPIKEY` with your API key,  `QUERYPARAMETERS` with parameters as it is defined in API and YOURDOMAIN with domainname from which you will make requests for example asdf.com.

Each project has different API key. Before making any request with your api key please be sure you configured allowed titles in [admin](https://affwebgen.com).

To make any request use api url: <code>https://affwebgen.com/api</code> and send us <code>GET</code> request.

<aside class="notice">
    You must replace <code>YOURAPIKEY</code> with your API key  and <code>YOURDOMAIN</code> with your domain name from your project in admin.
</aside>

# Query Parameters
Query parameters are used to generated specific response. You can combine it in any way you want. Every response is JSON formated.
## Extra
> Request:

```php
<?php
$query_parameters = [
    'extra' => [
        ['function' => 'popularBooks', 'parameters' => ['limit' => 1], 'properties' => ['imageSrc']],
        ['function' => 'latestBooks', 'parameters' => ['limit' => 2], 'properties' => ['imageSrc', 'pages']],
    ],
];

?>
```


> Response:

```json
{
  "extra": {
    "popularBooks": [
      {
        "id": 1,
        "name": "The Lord of the Rings",
        "slug": "the-lord-of-the-rings",
        "imageSrc": "https://i.gr-assets.com/images/S/compressed.photo.goodreads.com/books/1547450792i/33.jpg"
      }
    ],
    "latestBooks": [
      {
        "id": 1,
        "name": "The Lord of the Rings",
        "slug": "the-lord-of-the-rings",
        "imageSrc": "https://i.gr-assets.com/images/S/compressed.photo.goodreads.com/books/1547450792i/33.jpg",
        "pages": 1216
      },
      {
        "id": 2,
        "name": "The Lord of the Rings",
        "slug": "the-lord-of-the-rings",
        "imageSrc": "https://images.gr-assets.com/books/1330855500l/13510444.jpg",
        "pages": 1220
      }
    ]
  }
}

```


    Required: false
    <table class="table table-responsive">
        <tr>
            <th>Function</th>
            <th>Parameters</th>
            <th>Properties</th>
            <th>Description</th>
        </tr>
                    <tr>
                <td>popularBooks</td>
                <td>
                                                                            <div><span>**Name:** </span>limit</div>
    <div><span>**Required:** </span> yes </div>
    <div><span>**Type:** </span>int</div>
    <div><span>**Max value:** </span>10</div>
    
                                                            </td>
                <td>
                                                <div><span>**Default:** </span>id, name, slug</div>
    <div><span>**Valid Options:** </span>id, name, description, imageSrc, isbn10, isbn13, asin10, externalUrl, pages, rating, releasedYear, releasedMonth, releasedDay, firstReleasedYear, firstReleasedMonth, firstReleasedDay, slug, format, language</div>

                                    </td>
                <td>
                    list of popular books
                </td>
            </tr>
                    <tr>
                <td>latestBooks</td>
                <td>
                                                                            <div><span>**Name:** </span>limit</div>
    <div><span>**Required:** </span> yes </div>
    <div><span>**Type:** </span>int</div>
    <div><span>**Max value:** </span>10</div>
    
                                                            </td>
                <td>
                                                <div><span>**Default:** </span>id, name, slug</div>
    <div><span>**Valid Options:** </span>id, name, description, imageSrc, isbn10, isbn13, asin10, externalUrl, pages, rating, releasedYear, releasedMonth, releasedDay, firstReleasedYear, firstReleasedMonth, firstReleasedDay, slug, format, language</div>

                                    </td>
                <td>
                    list of latest books
                </td>
            </tr>
            </table>







## Item (book)
> Request:

```php
<?php
$query_parameters = [
    'item' => [
        'id' => 2,
        'entity' => 'Book',
    ],
];

?>
```


> Response:

```json
{
  "item": {
    "id": 2,
    "name": "The Lord of the Rings",
    "slug": "the-lord-of-the-rings"
  }
}

```


    Required: false

    <table class="table table-responsive">
        <tr>
            <th>Parameter</th>
            <th>Required</th>
            <th>Allowed Values</th>
            <th>Format</th>
            <th>Description</th>
        </tr>
                    <tr>
                <td>entity</td>
                <td>                        yes
                                    </td>
                <td>
                                            Book
                                    </td>
                <td>
                    string
                </td>
                <td>static text, identify collection</td>
            </tr>
                    <tr>
                <td>id</td>
                <td>                        yes
                                    </td>
                <td>
                                                        </td>
                <td>
                    integer
                </td>
                <td>the ID of major book</td>
            </tr>
                    <tr>
                <td>properties</td>
                <td>                        no
                                    </td>
                <td>
                                                                        <a href="#properties">properties</a>
                                                            </td>
                <td>
                    array
                </td>
                <td>array of properties</td>
            </tr>
                    <tr>
                <td>relations</td>
                <td>                        no
                                    </td>
                <td>
                                                                        <a href="#relations">relations</a>
                                                            </td>
                <td>
                    array
                </td>
                <td>array of relations</td>
            </tr>
                    <tr>
                <td>methods</td>
                <td>                        no
                                    </td>
                <td>
                                                                        <a href="#methods">methods</a>
                                                            </td>
                <td>
                    array
                </td>
                <td>array of methods</td>
            </tr>
            </table>



### Properties
> Request:

```php
<?php
$query_parameters = [
    'item' => [
        'id' => 2,
        'entity' => 'Book',
        'properties' => [
            'id', 'name', 'description', 'imageSrc', 'isbn10', 'isbn13', 'asin10', 'externalUrl', 'pages', 'rating',
            'releasedYear', 'releasedMonth', 'releasedDay', 'firstReleasedYear', 'firstReleasedMonth', 'firstReleasedDay', 'slug',
        ],
    ],
];

?>
```


> Response:

```json
{
  "item": {
    "id": 2,
    "name": "The Lord of the Rings",
    "slug": "the-lord-of-the-rings",
    "description": "One Ring to rule them all, One Ring to find them, One Ring to bring them all and in the darkness bind them<br><br>In ancient times the Rings of Power were crafted by the Elven-smiths, and Sauron, the Dark Lord, forged the One Ring, filling it with his own power so that he could rule all others. But the One Ring was taken from him, and though he sought it throughout Middle-earth, it remained lost to him. After many ages it fell by chance into the hands of the hobbit Bilbo Baggins.<br><br>From Sauron's fastness in the Dark Tower of Mordor, his power spread far and wide. Sauron gathered all the Great Rings to him, but always he searched for the One Ring that would complete his dominion.<br><br>When Bilbo reached his eleventy-first birthday he disappeared, bequeathing to his young cousin Frodo the Ruling Ring and a perilous quest: to journey across Middle-earth, deep into the shadow of the Dark Lord, and destroy the Ring by casting it into the Cracks of Doom.<br><br>The Lord of the Rings tells of the great quest undertaken by Frodo and the Fellowship of the Ring: Gandalf the Wizard; the hobbits Merry, Pippin, and Sam; Gimli the Dwarf; Legolas the Elf; Boromir of Gondor; and a tall, mysterious stranger called Strider.<br><br>This new edition includes the fiftieth-anniversary fully corrected text setting and, for the first time, an extensive new index.<br><br>J.R.R. Tolkien (1892-1973), beloved throughout the world as the creator of The Hobbit, The Lord of the Rings, and The Silmarillion, was a professor of Anglo-Saxon at Oxford, a fellow of Pembroke College, and a fellow of Merton College until his retirement in 1959. His chief interest was the linguistic aspects of the early English written tradition, but while he studied classic works of the past, he was creating a set of his own.",
    "imageSrc": "https://images.gr-assets.com/books/1330855500l/13510444.jpg",
    "isbn10": null,
    "isbn13": null,
    "asin10": "B007978OY6",
    "externalUrl": null,
    "pages": 1220,
    "rating": {
      "value": "4.49",
      "weight": 497395,
      "scale": 5
    },
    "releasedYear": 2012,
    "releasedMonth": 2,
    "releasedDay": 15,
    "firstReleasedYear": 1955,
    "firstReleasedMonth": 10,
    "firstReleasedDay": 20
  }
}

```


    <table>
        <thead>
            <tr>
                <th>Default</th>
                <th>Valid Options</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>id, name, slug</td>
                <td>id, name, description, imageSrc, isbn10, isbn13, asin10, externalUrl, pages, rating, releasedYear, releasedMonth, releasedDay, firstReleasedYear, firstReleasedMonth, firstReleasedDay, slug, format, language</td>
            </tr>
        </tbody>
    </table>




### Relations
> Request:

```php
<?php
$query_parameters = [
    'item' => [
        'id' => 2,
        'entity' => 'Book',
        'relations' => [
            'awards' =>  ['parameters' => ['limit' => 1]],
            'characters' => ['parameters' => ['limit' => 1]],
            'genres' =>  ['parameters' => ['limit' => 2]],
            'persons' =>  ['parameters' => ['limit' => 1]],
            'places' =>  ['parameters' => ['limit' => 1]],
            'series' =>  ['parameters' => ['limit' => 1]],
        ],
    ],
];

?>
```


> Response:

```json
{
  "item": {
    "id": 2,
    "name": "The Lord of the Rings",
    "slug": "the-lord-of-the-rings",
    "awards": [
      {
        "id": 1,
        "name": "Hugo Award Nominee for Best All-Time Series (1966)"
      }
    ],
    "characters": [
      {
        "id": 1,
        "name": "Frodo Baggins"
      }
    ],
    "genres": [
      {
        "id": 1,
        "name": "Fantasy"
      },
      {
        "id": 2,
        "name": "Classics"
      }
    ],
    "persons": [
      {
        "id": 1,
        "name": "J.R.R. Tolkien"
      }
    ],
    "places": [
      {
        "id": 1,
        "name": "Middle-earth"
      }
    ],
    "series": [
      {
        "id": 1,
        "name": "Middle-Earth Universe"
      }
    ]
  }
}

```


    <table class="table table-responsive">
        <tr>
            <th>Function</th>
            <th>Parameters</th>
            <th>Properties</th>
            <th>Description</th>
        </tr>
                    <tr>
                <td>awards</td>
                <td>
                                                                            <div><span>**Name:** </span>limit</div>
    <div><span>**Required:** </span> yes </div>
    <div><span>**Type:** </span>int</div>
    <div><span>**Max value:** </span>5</div>
    
                                                            </td>
                <td>
                                                <div><span>**Default:** </span>id, name</div>
    <div><span>**Valid Options:** </span>id, name</div>

                                    </td>
                <td>
                    list of awards
                </td>
            </tr>
                    <tr>
                <td>characters</td>
                <td>
                                                                            <div><span>**Name:** </span>limit</div>
    <div><span>**Required:** </span> yes </div>
    <div><span>**Type:** </span>int</div>
    <div><span>**Max value:** </span>20</div>
    
                                                            </td>
                <td>
                                                <div><span>**Default:** </span>id, name</div>
    <div><span>**Valid Options:** </span>id, name</div>

                                    </td>
                <td>
                    list of characters
                </td>
            </tr>
                    <tr>
                <td>genres</td>
                <td>
                                                                            <div><span>**Name:** </span>limit</div>
    <div><span>**Required:** </span> yes </div>
    <div><span>**Type:** </span>int</div>
    <div><span>**Max value:** </span>5</div>
    
                                                            </td>
                <td>
                                                <div><span>**Default:** </span>id, name</div>
    <div><span>**Valid Options:** </span>id, name</div>

                                    </td>
                <td>
                    list of genres
                </td>
            </tr>
                    <tr>
                <td>persons</td>
                <td>
                                                                            <div><span>**Name:** </span>limit</div>
    <div><span>**Required:** </span> yes </div>
    <div><span>**Type:** </span>int</div>
    <div><span>**Max value:** </span>5</div>
    
                                                            </td>
                <td>
                                                <div><span>**Default:** </span>id, name</div>
    <div><span>**Valid Options:** </span>id, name, imageSrc, description, followers</div>

                                    </td>
                <td>
                    list of persons
                </td>
            </tr>
                    <tr>
                <td>places</td>
                <td>
                                                                            <div><span>**Name:** </span>limit</div>
    <div><span>**Required:** </span> yes </div>
    <div><span>**Type:** </span>int</div>
    <div><span>**Max value:** </span>5</div>
    
                                                            </td>
                <td>
                                                <div><span>**Default:** </span>id, name</div>
    <div><span>**Valid Options:** </span>id, name</div>

                                    </td>
                <td>
                    list of places
                </td>
            </tr>
                    <tr>
                <td>series</td>
                <td>
                                                                            <div><span>**Name:** </span>limit</div>
    <div><span>**Required:** </span> yes </div>
    <div><span>**Type:** </span>int</div>
    <div><span>**Max value:** </span>5</div>
    
                                                            </td>
                <td>
                                                <div><span>**Default:** </span>id, name</div>
    <div><span>**Valid Options:** </span>id, name</div>

                                    </td>
                <td>
                    list of series
                </td>
            </tr>
            </table>






### Methods
> Request:

```php
<?php
$query_parameters = [
    'item' => [
        'id' => 2,
        'entity' => 'Book',
        'methods' => [
            ['function' => 'otherBooks', 'parameters' => ['limit' => 1], 'properties' => ['imageSrc', 'isbn10', 'isbn13', 'asin10',]],
        ],
    ],
];

?>
```


> Response:

```json
{
  "item": {
    "id": 2,
    "name": "The Lord of the Rings",
    "slug": "the-lord-of-the-rings",
    "otherBooks": [
      {
        "id": 3,
        "name": "The Lord of the Rings",
        "slug": "the-lord-of-the-rings",
        "imageSrc": "https://images.gr-assets.com/books/1296933438l/15350.jpg",
        "isbn10": null,
        "isbn13": null,
        "asin10": null
      }
    ]
  }
}

```


    <table class="table table-responsive">
        <tr>
            <th>Function</th>
            <th>Parameters</th>
            <th>Properties</th>
            <th>Description</th>
        </tr>
                    <tr>
                <td>otherBooks</td>
                <td>
                                                                            <div><span>**Name:** </span>limit</div>
    <div><span>**Required:** </span> yes </div>
    <div><span>**Type:** </span>int</div>
    <div><span>**Max value:** </span>10</div>
    
                                                            </td>
                <td>
                                                <div><span>**Default:** </span>id, name, slug</div>
    <div><span>**Valid Options:** </span>id, name, description, imageSrc, isbn10, isbn13, asin10, externalUrl, pages, rating, releasedYear, releasedMonth, releasedDay, firstReleasedYear, firstReleasedMonth, firstReleasedDay, slug, format, language</div>

                                    </td>
                <td>
                    other titles based on major title
                </td>
            </tr>
            </table>





### Full Example (book)
> Request:

```php
<?php
$query_parameters = [
    'item' => [
        'id' => 2,
        'entity' => 'Book',
        'properties' => [
            'id', 'name', 'description', 'imageSrc', 'isbn10', 'isbn13', 'asin10', 'externalUrl', 'pages', 'rating',
            'releasedYear', 'releasedMonth', 'releasedDay', 'firstReleasedYear', 'firstReleasedMonth', 'firstReleasedDay', 'slug',
        ],
        'relations' => [
            'awards' =>  ['parameters' => ['limit' => 1]],
            'characters' => ['parameters' => ['limit' => 1]],
            'genres' =>  ['parameters' => ['limit' => 2]],
            'persons' =>  ['parameters' => ['limit' => 1]],
            'places' =>  ['parameters' => ['limit' => 1]],
            'series' =>  ['parameters' => ['limit' => 1]],
        ],
        'methods' => [
            ['function' => 'otherBooks', 'parameters' => ['limit' => 1], 'properties' => ['imageSrc', 'isbn10', 'isbn13', 'asin10',]],
        ],
    ],
    'extra' => [
        ['function' => 'popularBooks', 'parameters' => ['limit' => 1], 'properties' => ['imageSrc']],
        ['function' => 'latestBooks', 'parameters' => ['limit' => 2], 'properties' => ['imageSrc', 'pages']],
    ],
];
$api_key = YOURAPIKEY;
$host = YOURDOMAIN;

$httpClient = HttpClient::create([
    'headers' => ['X-AUTH-API' => $api_key, 'Referer' => $host],
]);

$response = $httpClient->request('GET', 'https://affwebgen.com/api', ['query' => $query_parameters,]);

?>
```


> Response:

```json
{
  "item": {
    "id": 2,
    "name": "The Lord of the Rings",
    "slug": "the-lord-of-the-rings",
    "description": "One Ring to rule them all, One Ring to find them, One Ring to bring them all and in the darkness bind them<br><br>In ancient times the Rings of Power were crafted by the Elven-smiths, and Sauron, the Dark Lord, forged the One Ring, filling it with his own power so that he could rule all others. But the One Ring was taken from him, and though he sought it throughout Middle-earth, it remained lost to him. After many ages it fell by chance into the hands of the hobbit Bilbo Baggins.<br><br>From Sauron's fastness in the Dark Tower of Mordor, his power spread far and wide. Sauron gathered all the Great Rings to him, but always he searched for the One Ring that would complete his dominion.<br><br>When Bilbo reached his eleventy-first birthday he disappeared, bequeathing to his young cousin Frodo the Ruling Ring and a perilous quest: to journey across Middle-earth, deep into the shadow of the Dark Lord, and destroy the Ring by casting it into the Cracks of Doom.<br><br>The Lord of the Rings tells of the great quest undertaken by Frodo and the Fellowship of the Ring: Gandalf the Wizard; the hobbits Merry, Pippin, and Sam; Gimli the Dwarf; Legolas the Elf; Boromir of Gondor; and a tall, mysterious stranger called Strider.<br><br>This new edition includes the fiftieth-anniversary fully corrected text setting and, for the first time, an extensive new index.<br><br>J.R.R. Tolkien (1892-1973), beloved throughout the world as the creator of The Hobbit, The Lord of the Rings, and The Silmarillion, was a professor of Anglo-Saxon at Oxford, a fellow of Pembroke College, and a fellow of Merton College until his retirement in 1959. His chief interest was the linguistic aspects of the early English written tradition, but while he studied classic works of the past, he was creating a set of his own.",
    "imageSrc": "https://images.gr-assets.com/books/1330855500l/13510444.jpg",
    "isbn10": null,
    "isbn13": null,
    "asin10": "B007978OY6",
    "externalUrl": null,
    "pages": 1220,
    "rating": {
      "value": "4.49",
      "weight": 497395,
      "scale": 5
    },
    "releasedYear": 2012,
    "releasedMonth": 2,
    "releasedDay": 15,
    "firstReleasedYear": 1955,
    "firstReleasedMonth": 10,
    "firstReleasedDay": 20,
    "awards": [
      {
        "id": 1,
        "name": "Hugo Award Nominee for Best All-Time Series (1966)"
      }
    ],
    "characters": [
      {
        "id": 1,
        "name": "Frodo Baggins"
      }
    ],
    "genres": [
      {
        "id": 1,
        "name": "Fantasy"
      },
      {
        "id": 2,
        "name": "Classics"
      }
    ],
    "persons": [
      {
        "id": 1,
        "name": "J.R.R. Tolkien"
      }
    ],
    "places": [
      {
        "id": 1,
        "name": "Middle-earth"
      }
    ],
    "series": [
      {
        "id": 1,
        "name": "Middle-Earth Universe"
      }
    ],
    "otherBooks": [
      {
        "id": 3,
        "name": "The Lord of the Rings",
        "slug": "the-lord-of-the-rings",
        "imageSrc": "https://images.gr-assets.com/books/1296933438l/15350.jpg",
        "isbn10": null,
        "isbn13": null,
        "asin10": null
      }
    ]
  },
  "extra": {
    "popularBooks": [
      {
        "id": 1,
        "name": "The Lord of the Rings",
        "slug": "the-lord-of-the-rings",
        "imageSrc": "https://i.gr-assets.com/images/S/compressed.photo.goodreads.com/books/1547450792i/33.jpg"
      }
    ],
    "latestBooks": [
      {
        "id": 1,
        "name": "The Lord of the Rings",
        "slug": "the-lord-of-the-rings",
        "imageSrc": "https://i.gr-assets.com/images/S/compressed.photo.goodreads.com/books/1547450792i/33.jpg",
        "pages": 1216
      },
      {
        "id": 2,
        "name": "The Lord of the Rings",
        "slug": "the-lord-of-the-rings",
        "imageSrc": "https://images.gr-assets.com/books/1330855500l/13510444.jpg",
        "pages": 1220
      }
    ]
  }
}

```

Working example with full configuration for book
## Item (person)
> Request:

```php
<?php
$query_parameters = [
    'item' => [
        'id' => 1376,
        'entity' => 'Person',
    ],
];

?>
```


> Response:

```json
{
  "item": {
    "id": 1376,
    "name": "Stephen King"
  }
}

```


    Required: false

    <table class="table table-responsive">
        <tr>
            <th>Parameter</th>
            <th>Required</th>
            <th>Allowed Values</th>
            <th>Format</th>
            <th>Description</th>
        </tr>
                    <tr>
                <td>entity</td>
                <td>                        yes
                                    </td>
                <td>
                                            Person
                                    </td>
                <td>
                    string
                </td>
                <td>static text, identify collection</td>
            </tr>
                    <tr>
                <td>id</td>
                <td>                        yes
                                    </td>
                <td>
                                                        </td>
                <td>
                    integer
                </td>
                <td>the ID of major person</td>
            </tr>
                    <tr>
                <td>properties</td>
                <td>                        no
                                    </td>
                <td>
                                                                        <a href="#properties-2">properties</a>
                                                            </td>
                <td>
                    array
                </td>
                <td>array of properties</td>
            </tr>
                    <tr>
                <td>methods</td>
                <td>                        no
                                    </td>
                <td>
                                                                        <a href="#methods-2">methods</a>
                                                            </td>
                <td>
                    array
                </td>
                <td>array of methods</td>
            </tr>
            </table>



### Properties
> Request:

```php
<?php
$query_parameters = [
    'item' => [
        'id' => 1376,
        'entity' => 'Person',
        'properties' => [
            'id', 'name', 'imageSrc', 'description', 'followers'
        ],
    ],
];

?>
```


> Response:

```json
{
  "item": {
    "id": 1376,
    "name": "Stephen King",
    "imageSrc": "https://images.gr-assets.com/authors/1362814142p3/3389.jpg",
    "description": "Stephen Edwin King was born the second son of Donald and Nellie Ruth Pillsbury King. After his father left them when Stephen was two, he and his older brother, David, were raised by his mother. Parts of his childhood were spent in Fort Wayne, Indiana, where his father's family was at the time, and in Stratford, Connecticut. When Stephen was eleven, his mother brought her children back to Durham, Maine, for good. Her parents, Guy and Nellie Pillsbury, had become incapacitated with old age, and Ruth King was persuaded by her sisters to take over the physical care of them. Other family members provided a small house in Durham and financial support. After Stephen's grandparents passed away, Mrs. King found work in the kitchens of Pineland, a nearby residential facility for the mentally challenged.<br><br>Stephen attended the grammar school in Durham and Lisbon Falls High School, graduating in 1966. From his sophomore year at the University of Maine at Orono, he wrote a weekly column for the school newspaper, THE MAINE CAMPUS. He was also active in student politics, serving as a member of the Student Senate. He came to support the anti-war movement on the Orono campus, arriving at his stance from a conservative view that the war in Vietnam was unconstitutional. He graduated in 1970, with a B.A. in English and qualified to teach on the high school level. A draft board examination immediately post-graduation found him 4-F on grounds of high blood pressure, limited vision, flat feet, and punctured eardrums.<br><br>He met Tabitha Spruce in the stacks of the Fogler Library at the University, where they both worked as students; they married in January of 1971. As Stephen was unable to find placement as a teacher immediately, the Kings lived on his earnings as a laborer at an industrial laundry, and her student loan and savings, with an occasional boost from a short story sale to men's magazines.<br><br>Stephen made his first professional short story sale (\"The Glass Floor\") to Startling Mystery Stories in 1967. Throughout the early years of his marriage, he continued to sell stories to men's magazines. Many were gathered into the Night Shift collection or appeared in other anthologies.<br><br>In the fall of 1971, Stephen began teaching English at Hampden Academy, the public high school in Hampden, Maine. Writing in the evenings and on the weekends, he continued to produce short stories and to work on novels.",
    "followers": 630580
  }
}

```


    <table>
        <thead>
            <tr>
                <th>Default</th>
                <th>Valid Options</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>id, name</td>
                <td>id, name, imageSrc, description, followers</td>
            </tr>
        </tbody>
    </table>





### Methods
> Request:

```php
<?php
$query_parameters = [
    'item' => [
        'id' => 1376,
        'entity' => 'Person',
        'methods' => [
            ['function' => 'otherBooks', 'parameters' => ['limit' => 1], 'properties' => ['imageSrc', 'isbn10',]],
        ],
    ],
];

?>
```


> Response:

```json
{
  "item": {
    "id": 1376,
    "name": "Stephen King",
    "otherBooks": [
      {
        "id": 1376,
        "name": "Pilgrim's Progress, Part 2: Christiana",
        "slug": "pilgrim-s-progress-part-2-christiana",
        "imageSrc": "https://images.gr-assets.com/books/1352964261l/1140624.jpg",
        "isbn10": "0768422531"
      }
    ]
  }
}

```


    <table class="table table-responsive">
        <tr>
            <th>Function</th>
            <th>Parameters</th>
            <th>Properties</th>
            <th>Description</th>
        </tr>
                    <tr>
                <td>otherBooks</td>
                <td>
                                                                            <div><span>**Name:** </span>limit</div>
    <div><span>**Required:** </span> yes </div>
    <div><span>**Type:** </span>int</div>
    <div><span>**Max value:** </span>30</div>
    
                                                            </td>
                <td>
                                                <div><span>**Default:** </span>id, name, slug</div>
    <div><span>**Valid Options:** </span>id, name, description, imageSrc, isbn10, isbn13, asin10, externalUrl, pages, rating, releasedYear, releasedMonth, releasedDay, firstReleasedYear, firstReleasedMonth, firstReleasedDay, slug, format, language</div>

                                    </td>
                <td>
                    books from major person
                </td>
            </tr>
            </table>





### Full Example (person)
> Request:

```php
<?php
$query_parameters = [
    'item' => [
        'id' => 1376,
        'entity' => 'Person',
        'methods' => [
            ['function' => 'otherBooks', 'parameters' => ['limit' => 1], 'properties' => ['imageSrc', 'isbn10',]],
        ],
        'properties' => [
            'id', 'name', 'imageSrc', 'description', 'followers'
        ],
    ],
    'extra' => [
        ['function' => 'popularBooks', 'parameters' => ['limit' => 1], 'properties' => ['imageSrc']],
        ['function' => 'latestBooks', 'parameters' => ['limit' => 2], 'properties' => ['imageSrc', 'pages']],
    ],
];
$api_key = YOURAPIKEY;
$host = YOURDOMAIN;

$httpClient = HttpClient::create([
    'headers' => ['X-AUTH-API' => $api_key, 'Referer' => $host],
]);

$response = $httpClient->request('GET', 'https://affwebgen.com/api', ['query' => $query_parameters,]);

?>
```


> Response:

```json
{
  "item": {
    "id": 1376,
    "name": "Stephen King",
    "imageSrc": "https://images.gr-assets.com/authors/1362814142p3/3389.jpg",
    "description": "Stephen Edwin King was born the second son of Donald and Nellie Ruth Pillsbury King. After his father left them when Stephen was two, he and his older brother, David, were raised by his mother. Parts of his childhood were spent in Fort Wayne, Indiana, where his father's family was at the time, and in Stratford, Connecticut. When Stephen was eleven, his mother brought her children back to Durham, Maine, for good. Her parents, Guy and Nellie Pillsbury, had become incapacitated with old age, and Ruth King was persuaded by her sisters to take over the physical care of them. Other family members provided a small house in Durham and financial support. After Stephen's grandparents passed away, Mrs. King found work in the kitchens of Pineland, a nearby residential facility for the mentally challenged.<br><br>Stephen attended the grammar school in Durham and Lisbon Falls High School, graduating in 1966. From his sophomore year at the University of Maine at Orono, he wrote a weekly column for the school newspaper, THE MAINE CAMPUS. He was also active in student politics, serving as a member of the Student Senate. He came to support the anti-war movement on the Orono campus, arriving at his stance from a conservative view that the war in Vietnam was unconstitutional. He graduated in 1970, with a B.A. in English and qualified to teach on the high school level. A draft board examination immediately post-graduation found him 4-F on grounds of high blood pressure, limited vision, flat feet, and punctured eardrums.<br><br>He met Tabitha Spruce in the stacks of the Fogler Library at the University, where they both worked as students; they married in January of 1971. As Stephen was unable to find placement as a teacher immediately, the Kings lived on his earnings as a laborer at an industrial laundry, and her student loan and savings, with an occasional boost from a short story sale to men's magazines.<br><br>Stephen made his first professional short story sale (\"The Glass Floor\") to Startling Mystery Stories in 1967. Throughout the early years of his marriage, he continued to sell stories to men's magazines. Many were gathered into the Night Shift collection or appeared in other anthologies.<br><br>In the fall of 1971, Stephen began teaching English at Hampden Academy, the public high school in Hampden, Maine. Writing in the evenings and on the weekends, he continued to produce short stories and to work on novels.",
    "followers": 630580,
    "otherBooks": [
      {
        "id": 1376,
        "name": "Pilgrim's Progress, Part 2: Christiana",
        "slug": "pilgrim-s-progress-part-2-christiana",
        "imageSrc": "https://images.gr-assets.com/books/1352964261l/1140624.jpg",
        "isbn10": "0768422531"
      }
    ]
  },
  "extra": {
    "popularBooks": [
      {
        "id": 1,
        "name": "The Lord of the Rings",
        "slug": "the-lord-of-the-rings",
        "imageSrc": "https://i.gr-assets.com/images/S/compressed.photo.goodreads.com/books/1547450792i/33.jpg"
      }
    ],
    "latestBooks": [
      {
        "id": 1,
        "name": "The Lord of the Rings",
        "slug": "the-lord-of-the-rings",
        "imageSrc": "https://i.gr-assets.com/images/S/compressed.photo.goodreads.com/books/1547450792i/33.jpg",
        "pages": 1216
      },
      {
        "id": 2,
        "name": "The Lord of the Rings",
        "slug": "the-lord-of-the-rings",
        "imageSrc": "https://images.gr-assets.com/books/1330855500l/13510444.jpg",
        "pages": 1220
      }
    ]
  }
}

```

Working example with full configuration for person


