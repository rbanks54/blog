---
title: 'Instagram API filtering (or querying)'
date: 2014-02-21T16:53:00.000+11:00
draft: false
tags : [regex, json, facebook api, python, instagraph api]
---

[GitHub](https://github.com/RaphHaddad/IgAPIFiltering)  
  
Instagram's APIs are well written, well documented, RESTfull and simply a breeze to use.  
  
I myself prefer them to the Facebook APIs, however the Facebook Graph API does have an advantage over that of the Instagram API - namely filtering. The question I will answer in this blog post is whether there is an efficient way to filter the Instagram API.  
  

### Facebook Situation

For example, if I wanted to display information about a user on Facebook, I would query:  
  

/4  

  
The result would yield the result  
  

{  
  "id": "4",   
  "name": "Mark Zuckerberg",   
  "first_name": "Mark",   
  "last_name": "Zuckerberg",   
  "link": "https://www.facebook.com/zuck",   
  "hometown": {  
    "id": "105506396148790",   
    "name": "Dobbs Ferry, New York"  
  },   
  "location": {  
    "id": "104022926303756",   
    "name": "Palo Alto, California"  
  },   
  "bio": "I'm trying to make the world a more open place.",   
  "quotes": "\\"Fortune favors the bold.\\"\\r\\n- Virgil, Aeneid X.284\\r\\n\\r\\n\\"All children are artists. The problem is how to remain an artist once you grow up.\\" \\r\\n- Pablo Picasso\\r\\n\\r\\n\\"Make things as simple as possible but no simpler.\\"\\r\\n- Albert Einstein",   
  "work": \[  
    {  
      "employer": {  
        "id": "20531316728",   
        "name": "Facebook"  
      },   
      "location": {  
        "id": "104022926303756",   
        "name": "Palo Alto, California"  
      },   
      "position": {  
        "id": "142979352398617",   
        "name": "Founder and CEO"  
      },   
      "description": "Making the world more open and connected.",   
      "start_date": "2004-02-04"  
    }  
  \],   
  ...  

  "gender": "male",   
  "locale": "en_US",   
  "languages": \[  
    {  
      "id": "106059522759137",   
      "name": "English"  
    },   
    {  
      "id": "103088979730830",   
      "name": "Mandarin Chinese"  
    }  
  \],   
  "updated_time": "2013-12-11T23:12:52+0000",   
  "username": "zuck"  
}  

  
  
Now, if I wanted to filter by specific fields. I could simply query.  
  

/4?fields=name,id,link  

  
and the result would be  
  
  

{  
  "name": "Mark Zuckerberg",   
  "id": "4",   
  "link": "https://www.facebook.com/zuck"  
}  

  
And what's even cooler is the Facebook Query Language (FQL) which allows you to do more complicated queries, using many of the features of SQL. Here is an example:  
  

SELECT first\_name, last\_name from user where uid =4 ;  

  
this would result in the response:  
  
  

{  
  "data": \[  
    {  
      "first_name": "Mark",   
      "last_name": "Zuckerberg"  
    }  
  \]  
}  

  
All of these may be tested with an access token or alternatively using the [Graph API Explorer](https://developers.facebook.com/tools/explorer/). I will also blog about more complicated Facebook Queries in the near future.  

### Instagram Solution

The Instagram API does not contain these filtering features. That is, if we want data of one specific person, at a specific location we would need to use the _location_ api and traverse every record to check if the specific person exists. In addition to this, **the Instagram API has a limit on how many records are displayed per call**, meaning that not all the records can be viewed at one time.  
  
Using the Facebook Graph API (or FQL) we simply pass an extremely large limit.

  

For example getting a subset of people who have tagged the_ Rag and Famish_ we would call:

  

/locations/604145/media/recent  

  
this would yield  
  

{  
    "pagination": {  
        "next_url": "https://api.instagram.com/v1/locations/604145/media/recent?max\_id=645281964529741622&client\_id=f0f2f52cb6d046d68ded60b896bb0428",  
        "next\_max\_id": "645281964529741622"  
    },  
    "meta": {  
        "code": 200  
    },  
    "data": \[

        {  
            "attribution": null,  
            "tags": \[  
                "regram",  
                "growlers",  
                "ragandfamish",  
                "draughtbeerathome",  
                "craftbeers"  
            \],  
            "location": {  
                "latitude": -33.836733742,  
                "name": "Rag and Famish Hotel",  
                "longitude": 151.207236114,  
                "id": 604145  
            },  
            "comments": {  
                "count": 0,  
                "data": \[\]  
            },  
            "filter": "Normal",  
            "created_time": "1392148936",  
            "link": "http://instagram.com/p/kSdm8Gwu2y/",  
            "likes": {  
                "count": 5,  
                "data": \[  
                    {  
                        "username": "kylierobertsfrost",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_197831255\_75sq_1385208925.jpg",  
                        "id": "197831255",  
                        "full_name": "kylierobertsfrost"  
                    },  
                    {  
                        "username": "sachandpete",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_195935360\_75sq_1372932809.jpg",  
                        "id": "195935360",  
                        "full_name": "sachandpete"  
                    },  
                    {  
                        "username": "robbiebarsman",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_749349673\_75sq_1386117520.jpg",  
                        "id": "749349673",  
                        "full_name": "Robbie Barsman"  
                    },  
                    {  
                        "username": "happyandhoppy",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_604192935\_75sq_1381672642.jpg",  
                        "id": "604192935",  
                        "full_name": "Happy & Hoppy"  
                    }  
                \]  
            },  
            "images": {  
                "low_resolution": {  
                    "url": "http://distilleryimage7.s3.amazonaws.com/12b0798a935711e3b4c6124d293a9c07_6.jpg",  
                    "width": 306,  
                    "height": 306  
                },  
                "thumbnail": {  
                    "url": "http://distilleryimage7.s3.amazonaws.com/12b0798a935711e3b4c6124d293a9c07_5.jpg",  
                    "width": 150,  
                    "height": 150  
                },  
                "standard_resolution": {  
                    "url": "http://distilleryimage7.s3.amazonaws.com/12b0798a935711e3b4c6124d293a9c07_8.jpg",  
                    "width": 640,  
                    "height": 640  
                }  
            },  
            "users\_in\_photo": \[\],  
            "caption": {  
                "created_time": "1392148936",  
                "text": "Best birthday present ever! Thanks @justinrob. #growlers #ragandfamish #regram #draughtbeerathome #craftbeers",  
                "from": {  
                    "username": "ragandfamish",  
                    "profile_picture": "http://images.ak.instagram.com/profiles/profile\_586799282\_75sq_1380774891.jpg",  
                    "id": "586799282",  
                    "full_name": "Rag and Famish"  
                },  
                "id": "653715115635567907"  
            },  
            "type": "image",  
            "id": "653715115149028786_586799282",  
            "user": {  
                "username": "ragandfamish",  
                "website": "",  
                "profile_picture": "http://images.ak.instagram.com/profiles/profile\_586799282\_75sq_1380774891.jpg",  
                "full_name": "Rag and Famish",  
                "bio": "",  
                "id": "586799282"  
            }  
        },  
        {  
            "attribution": null,  
            "tags": \[  
                "valentinesday",  
                "lovers",  
                "ragandfamish"  
            \],  
            "location": {  
                "latitude": -33.836733742,  
                "name": "Rag and Famish Hotel",  
                "longitude": 151.207236114,  
                "id": 604145  
            },  
            "comments": {  
                "count": 0,  
                "data": \[\]  
            },  
            "filter": "Normal",  
            "created_time": "1391992118",  
            "link": "http://instagram.com/p/kNygM3Qu36/",  
            "likes": {  
                "count": 1,  
                "data": \[  
                    {  
                        "username": "sachandpete",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_195935360\_75sq_1372932809.jpg",  
                        "id": "195935360",  
                        "full_name": "sachandpete"  
                    }  
                \]  
            },  
            "images": {  
                "low_resolution": {  
                    "url": "http://distilleryimage7.s3.amazonaws.com/9ec9080891e811e38f95121378c087a7_6.jpg",  
                    "width": 306,  
                    "height": 306  
                },  
                "thumbnail": {  
                    "url": "http://distilleryimage7.s3.amazonaws.com/9ec9080891e811e38f95121378c087a7_5.jpg",  
                    "width": 150,  
                    "height": 150  
                },  
                "standard_resolution": {  
                    "url": "http://distilleryimage7.s3.amazonaws.com/9ec9080891e811e38f95121378c087a7_8.jpg",  
                    "width": 640,  
                    "height": 640  
                }  
            },  
            "users\_in\_photo": \[\],  
            "caption": {  
                "created_time": "1391992118",  
                "text": "Part of our 4 Course Valentines menu...Grilled Swordfish in an Enoki Mushroom & Mussel Broth. #lovers #valentinesday #ragandfamish",  
                "from": {  
                    "username": "ragandfamish",  
                    "profile_picture": "http://images.ak.instagram.com/profiles/profile\_586799282\_75sq_1380774891.jpg",  
                    "id": "586799282",  
                    "full_name": "Rag and Famish"  
                },  
                "id": "652399637080239627"  
            },  
            "type": "image",  
            "id": "652399636199435770_586799282",  
            "user": {  
                "username": "ragandfamish",  
                "website": "",  
                "profile_picture": "http://images.ak.instagram.com/profiles/profile\_586799282\_75sq_1380774891.jpg",  
                "full_name": "Rag and Famish",  
                "bio": "",  
                "id": "586799282"  
            }  
        },  
        {  
            "attribution": null,  
            "tags": \[  
                "beer",  
                "growler",  
                "northsydney",  
                "publife",  
                "beerporn",  
                "sundaypublunch"  
            \],  
            "location": {  
                "latitude": -33.836733742,  
                "name": "Rag and Famish Hotel",  
                "longitude": 151.207236114,  
                "id": 604145  
            },  
            "comments": {  
                "count": 1,  
                "data": \[  
                    {  
                        "created_time": "1391940266",  
                        "text": "@ragandfamish #northsydney #publife #sundaypublunch #growler #beer #beerporn",  
                        "from": {  
                            "username": "justinrob",  
                            "profile_picture": "http://images.ak.instagram.com/profiles/profile\_989651\_75sq_1388267331.jpg",  
                            "id": "989651",  
                            "full_name": "Justin Roberts"  
                        },  
                        "id": "651964667522494700"  
                    }  
                \]  
            },  
            "filter": "Earlybird",  
            "created_time": "1391927371",  
            "link": "http://instagram.com/p/kL3AcXyLJc/",  
            "likes": {  
                "count": 11,  
                "data": \[  
                    {  
                        "username": "kylierobertsfrost",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_197831255\_75sq_1385208925.jpg",  
                        "id": "197831255",  
                        "full_name": "kylierobertsfrost"  
                    },  
                    {  
                        "username": "lakieshavictoria",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_540626969\_75sq_1390767554.jpg",  
                        "id": "540626969",  
                        "full_name": "Lakiesha"  
                    },  
                    {  
                        "username": "lightmoods",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_244107098\_75sq_1355083432.jpg",  
                        "id": "244107098",  
                        "full_name": "Paul Foley"  
                    },  
                    {  
                        "username": "jilltitle",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_192499308\_75sq_1377830018.jpg",  
                        "id": "192499308",  
                        "full_name": "Jill Title"  
                    }  
                \]  
            },  
            "images": {  
                "low_resolution": {  
                    "url": "http://distilleryimage7.s3.amazonaws.com/de5d60c2915211e3864a1248f379be2f_6.jpg",  
                    "width": 306,  
                    "height": 306  
                },  
                "thumbnail": {  
                    "url": "http://distilleryimage7.s3.amazonaws.com/de5d60c2915211e3864a1248f379be2f_5.jpg",  
                    "width": 150,  
                    "height": 150  
                },  
                "standard_resolution": {  
                    "url": "http://distilleryimage7.s3.amazonaws.com/de5d60c2915211e3864a1248f379be2f_8.jpg",  
                    "width": 640,  
                    "height": 640  
                }  
            },  
            "users\_in\_photo": \[\],  
            "caption": {  
                "created_time": "1391927371",  
                "text": "Lunch with the out-laws for Jacks B'day. Of course I had to buy him a growler!",  
                "from": {  
                    "username": "justinrob",  
                    "profile_picture": "http://images.ak.instagram.com/profiles/profile\_989651\_75sq_1388267331.jpg",  
                    "id": "989651",  
                    "full_name": "Justin Roberts"  
                },  
                "id": "651856494543287242"  
            },  
            "type": "image",  
            "id": "651856494107079260_989651",  
            "user": {  
                "username": "justinrob",  
                "website": "",  
                "profile_picture": "http://images.ak.instagram.com/profiles/profile\_989651\_75sq_1388267331.jpg",  
                "full_name": "Justin Roberts",  
                "bio": "",  
                "id": "989651"  
            }  
        },  
        {  
            "attribution": null,  
            "tags": \[  
                "lunch",  
                "ragandfamish",  
                "northsydney"  
            \],  
            "location": {  
                "latitude": -33.836733742,  
                "name": "Rag and Famish Hotel",  
                "longitude": 151.207236114,  
                "id": 604145  
            },  
            "comments": {  
                "count": 0,  
                "data": \[\]  
            },  
            "filter": "Normal",  
            "created_time": "1391652458",  
            "link": "http://instagram.com/p/kDqpzNskB3/",  
            "likes": {  
                "count": 17,  
                "data": \[  
                    {  
                        "username": "coffeeaspirin",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_28373215\_75sq_1360585473.jpg",  
                        "id": "28373215",  
                        "full_name": "coffeeaspirin"  
                    },  
                    {  
                        "username": "fumi_aji",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_37249123\_75sq_1387766058.jpg",  
                        "id": "37249123",  
                        "full_name": "fumi_aji"  
                    },  
                    {  
                        "username": "beckswg",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_181392294\_75sq_1356522218.jpg",  
                        "id": "181392294",  
                        "full_name": "beckswg"  
                    }  
                \]  
            },  
            "images": {  
                "low_resolution": {  
                    "url": "http://distilleryimage10.s3.amazonaws.com/593733d68ed311e387660e5ea1863fce_6.jpg",  
                    "width": 306,  
                    "height": 306  
                },  
                "thumbnail": {  
                    "url": "http://distilleryimage10.s3.amazonaws.com/593733d68ed311e387660e5ea1863fce_5.jpg",  
                    "width": 150,  
                    "height": 150  
                },  
                "standard_resolution": {  
                    "url": "http://distilleryimage10.s3.amazonaws.com/593733d68ed311e387660e5ea1863fce_8.jpg",  
                    "width": 640,  
                    "height": 640  
                }  
            },  
            "users\_in\_photo": \[\],  
            "caption": {  
                "created_time": "1391652458",  
                "text": "Team #lunch! #northsydney #ragandfamish",  
                "from": {  
                    "username": "coffeeaspirin",  
                    "profile_picture": "http://images.ak.instagram.com/profiles/profile\_28373215\_75sq_1360585473.jpg",  
                    "id": "28373215",  
                    "full_name": "coffeeaspirin"  
                },  
                "id": "649550362477478754"  
            },  
            "type": "image",  
            "id": "649550361714114679_28373215",  
            "user": {  
                "username": "coffeeaspirin",  
                "website": "",  
                "profile_picture": "http://images.ak.instagram.com/profiles/profile\_28373215\_75sq_1360585473.jpg",  
                "full_name": "coffeeaspirin",  
                "bio": "",  
                "id": "28373215"  
            }  
        },  
        {  
            "attribution": null,  
            "tags": \[  
                "healthylunch",  
                "longlunch",  
                "japaneseinspired",  
                "delish",  
                "salmon",  
                "ragandfamish",  
                "itsnearlytheweekend"  
            \],  
            "location": {  
                "latitude": -33.836733742,  
                "name": "Rag and Famish Hotel",  
                "longitude": 151.207236114,  
                "id": 604145  
            },  
            "comments": {  
                "count": 1,  
                "data": \[  
                    {  
                        "created_time": "1391648089",  
                        "text": "I had it yesterday. Amazing! ❤❤❤",  
                        "from": {  
                            "username": "soey01",  
                            "profile_picture": "http://images.ak.instagram.com/profiles/profile\_55967742\_75sq_1340531322.jpg",  
                            "id": "55967742",  
                            "full_name": "soey01"  
                        },  
                        "id": "649513705268243888"  
                    }  
                \]  
            },  
            "filter": "Normal",  
            "created_time": "1391647735",  
            "link": "http://instagram.com/p/kDhpQ-Qu-s/",  
            "likes": {  
                "count": 2,  
                "data": \[  
                    {  
                        "username": "sachandpete",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_195935360\_75sq_1372932809.jpg",  
                        "id": "195935360",  
                        "full_name": "sachandpete"  
                    },  
                    {  
                        "username": "xjenaleighx",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_403229736\_75sq_1385275310.jpg",  
                        "id": "403229736",  
                        "full_name": "JeNaLeigh"  
                    }  
                \]  
            },  
            "images": {  
                "low_resolution": {  
                    "url": "http://distilleryimage4.s3.amazonaws.com/5a2ea7c68ec711e3afc512c1a4977290_6.jpg",  
                    "width": 306,  
                    "height": 306  
                },  
                "thumbnail": {  
                    "url": "http://distilleryimage4.s3.amazonaws.com/5a2ea7c68ec711e3afc512c1a4977290_5.jpg",  
                    "width": 150,  
                    "height": 150  
                },  
                "standard_resolution": {  
                    "url": "http://distilleryimage4.s3.amazonaws.com/5a2ea7c68ec711e3afc512c1a4977290_8.jpg",  
                    "width": 640,  
                    "height": 640  
                }  
            },  
            "users\_in\_photo": \[\],  
            "caption": {  
                "created_time": "1391647735",  
                "text": "Perfect weather for a long lunch @ragandfamish. Try our Oven Baked Miso Salmon Fillet w cucumber, celery & wakame salad, on mashed potato and a soy & ginger sauce. #delish #healthylunch #longlunch #ragandfamish #salmon #japaneseinspired #itsnearlytheweekend",  
                "from": {  
                    "username": "ragandfamish",  
                    "profile_picture": "http://images.ak.instagram.com/profiles/profile\_586799282\_75sq_1380774891.jpg",  
                    "id": "586799282",  
                    "full_name": "Rag and Famish"  
                },  
                "id": "649510743066209558"  
            },  
            "type": "image",  
            "id": "649510742529339308_586799282",  
            "user": {  
                "username": "ragandfamish",  
                "website": "",  
                "profile_picture": "http://images.ak.instagram.com/profiles/profile\_586799282\_75sq_1380774891.jpg",  
                "full_name": "Rag and Famish",  
                "bio": "",  
                "id": "586799282"  
            }  
        },  
        {  
            "attribution": null,  
            "tags": \[  
                "getserious",  
                "tuesdaytrivia"  
            \],  
            "location": {  
                "latitude": -33.836733742,  
                "name": "Rag and Famish Hotel",  
                "longitude": 151.207236114,  
                "id": 604145  
            },  
            "comments": {  
                "count": 0,  
                "data": \[\]  
            },  
            "filter": "Mayfair",  
            "created_time": "1391504427",  
            "link": "http://instagram.com/p/j_QTlGIzbd/",  
            "likes": {  
                "count": 10,  
                "data": \[  
                    {  
                        "username": "india_e",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_44498065\_75sq_1373640663.jpg",  
                        "id": "44498065",  
                        "full_name": "India Edwards"  
                    },  
                    {  
                        "username": "lanaisadora",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_31316068\_75sq_1380689500.jpg",  
                        "id": "31316068",  
                        "full_name": "Lana Smith"  
                    },  
                    {  
                        "username": "indyhd",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_25219316\_75sq_1372308574.jpg",  
                        "id": "25219316",  
                        "full_name": "Ijhd"  
                    },  
                    {  
                        "username": "victoriaslessar",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_522809125\_75sq_1383365216.jpg",  
                        "id": "522809125",  
                        "full_name": "victoriaslessar"  
                    }  
                \]  
            },  
            "images": {  
                "low_resolution": {  
                    "url": "http://distilleryimage1.s3.amazonaws.com/ca9f0de68d7a11e3b1e712b84915c4bd_6.jpg",  
                    "width": 306,  
                    "height": 306  
                },  
                "thumbnail": {  
                    "url": "http://distilleryimage1.s3.amazonaws.com/ca9f0de68d7a11e3b1e712b84915c4bd_5.jpg",  
                    "width": 150,  
                    "height": 150  
                },  
                "standard_resolution": {  
                    "url": "http://distilleryimage1.s3.amazonaws.com/ca9f0de68d7a11e3b1e712b84915c4bd_8.jpg",  
                    "width": 640,  
                    "height": 640  
                }  
            },  
            "users\_in\_photo": \[  
                {  
                    "position": {  
                        "y": 0.423437506,  
                        "x": 0.287499994  
                    },  
                    "user": {  
                        "username": "charleethegirl",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_13826640\_75sq_1382712968.jpg",  
                        "id": "13826640",  
                        "full_name": "! charlotterose"  
                    }  
                },  
                {  
                    "position": {  
                        "y": 0.418749988,  
                        "x": 0.659375012  
                    },  
                    "user": {  
                        "username": "_calum2510",  
                        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_181622299\_75sq_1383456373.jpg",  
                        "id": "181622299",  
                        "full_name": "Calum Robertson"  
                    }  
                }  
            \],  
            "caption": {  
                "created_time": "1391504465",  
                "text": "I don't know where I find these people @charleethegirl @_calum2510 #tuesdaytrivia #getserious ✌️",  
                "from": {  
                    "username": "elm_evaclose",  
                    "profile_picture": "http://images.ak.instagram.com/profiles/profile\_199632252\_75sq_1392511005.jpg",  
                    "id": "199632252",  
                    "full_name": "Eva Close"  
                },  
                "id": "648308905367255001"  
            },  
            "type": "image",  
            "id": "648308585610295005_199632252",  
            "user": {  
                "username": "elm_evaclose",  
                "website": "",  
                "profile_picture": "http://images.ak.instagram.com/profiles/profile\_199632252\_75sq_1392511005.jpg",  
                "full_name": "Eva Close",  
                "bio": "",  
                "id": "199632252"  
            }  
        }

    \]  
}  

  
Notice the pagination? So to get all the data, we would need to create a function that simply gets all the data from Instagram. Unfortunately, there is no way around this other than making multiple calls. Below is an example. The key to this, is to keep on making requests until the **pagination** object is empty.  
  

yourClientId = "XXXX"

pages = "\["  
location = "604145"#Rag and Famish North Sydney!  
api = "https://api.instagram.com/v1/locations/{0}/media/recent?client_id={1}".format(location,yourClientId)  
print api  
while True:  
    r = requests.get(api)  
    instagramEnvelope =  r.json();  
    pagination = instagramEnvelope\["pagination"\]  
    if not pagination:  
        pages = pages\[:-1\]  
        break  
    pages += r.text  
    pages += ","  
    api = pagination\["next_url"\]  
pages += "\]"  

  
Now! I want to extract all the times a specific user (id=3419631) tagged a specific location (say the Rag and Famish id=604145). Using a traditional method I would need to traverse each object for comparison..  
  
Something similar to this:  
  

def iterateWay(igUserToFind):  
    pagesArray = json.loads(pages)  
    for page in pagesArray:  
        for location in page\["data"\]:  
            if location\["user"\]\["id"\] == igUserToFind:  
                print(datetime.datetime.fromtimestamp(int(location\["created_time"\])).strftime('%Y-%m-%d %H:%M:%S'))

#### The Solution

One word - Regex. I guess this whole blog post can be summarised in this one word.  
  
The Regex to extract a specific user would be  
  

"user":\\s+({\[^}\]+(("3419631"))\[^}\]+})  

  
The problem with this however, is that it only extracts a user JSON object. That is, it will only match an object below:  
  

            "user": {  
                "username": "lyntonmanuel",  
                "website": "",  
                "profile_picture": "http://images.ak.instagram.com/profiles/profile\_3419631\_75sq_1314210559.jpg",  
                "full_name": "Lynton Manuel",  
                "bio": "",  
                "id": "3419631"  
            }  

  
What we require as well, however, is the super object of this user object. That is, we require the object below:  
  

        {  
            "attribution": null,  
            "tags": \[\],  
            "location": {  
                "latitude": -33.836733742,  
                "name": "Rag and Famish Hotel",  
                "longitude": 151.207236114,  
                "id": 604145  
            },  
            "comments": {  
                "count": 0,  
                "data": \[\]  
            },  
            "filter": "Rise",  
            "created_time": "1320721905",  
            "link": "http://instagram.com/p/TOK6u/",  
            "likes": {  
                "count": 0,  
                "data": \[\]  
            },  
            "images": {  
                "low_resolution": {  
                    "url": "http://distilleryimage6.s3.amazonaws.com/63f931aa09b711e180c9123138016265_6.jpg",  
                    "width": 306,  
                    "height": 306  
                },  
                "thumbnail": {  
                    "url": "http://distilleryimage6.s3.amazonaws.com/63f931aa09b711e180c9123138016265_5.jpg",  
                    "width": 150,  
                    "height": 150  
                },  
                "standard_resolution": {  
                    "url": "http://distilleryimage6.s3.amazonaws.com/63f931aa09b711e180c9123138016265_7.jpg",  
                    "width": 612,  
                    "height": 612  
                }  
            },  
            "users\_in\_photo": \[\],  
            "caption": {  
                "created_time": "1320721933",  
                "text": "The 'Rag'",  
                "from": {  
                    "username": "lyntonmanuel",  
                    "profile_picture": "http://images.ak.instagram.com/profiles/profile\_3419631\_75sq_1314210559.jpg",  
                    "id": "3419631",  
                    "full_name": "Lynton Manuel"  
                },  
                "id": "403277727"  
            },  
            "type": "image",  
            "id": "322481838_3419631",  
            "user": {  
                "username": "lyntonmanuel",  
                "website": "",  
                "profile_picture": "http://images.ak.instagram.com/profiles/profile\_3419631\_75sq_1314210559.jpg",  
                "full_name": "Lynton Manuel",  
                "bio": "",  
                "id": "3419631"  
            }  
        }  

  
Using the object above (let's call it the location object), we can get information such as the time the user tagged the _Rag and Famish_. But how do we get the location object? We know that using Regex for hierarchical object is well.....simply evil.  
  
So how do we get the location object? First, let's make assumptions:  

1.  We assume that the User object will always be directly inside the location object. That is, it will be a directly child of the location object. With one degree of separation.
2.  We assume that the User object may be in any position inside the location object (that is, not the last object like the example above).
3.  That there is no '{' or '}' in the string parameters (although disregarding this wouldn't be too difficult)

The first step is extracting the user object. This is done as below:

  

def regexWay(igUserToFind):  
    p = re.compile(r'"user":\\s*({\[^}\]*(("'+igUserToFind+'"))\[^}\]*})',re.DOTALL)  
    for found in re.finditer(p,pages):  
        found.end()  

  

Here you can see that we find the exact position of the last character of the user object. That is, the enclosing '}'.  
  
The upcoming explanation assumes there will be character traversals in the whole string from Instagram.  
  
Now, because of assumption 1 we know that the object directly outside the user object is the location object. But if we traverse the string until we find a '}' we could fall into an error, **as there may be another object within the location object (remember assumption 2) after the user object**. for example, we could end up extracting a string like below if we simply traverse the string down to the next '}' character.

  

    "user": {  
        "username": "lyntonmanuel",  
        "website": "",  
        "profile_picture": "http://images.ak.instagram.com/profiles/profile\_3419631\_75sq_1314210559.jpg",  
        "full_name": "Lynton Manuel",  
        "bio": "",  
        "id": "3419631"  
    },  
    "Another": {  
        "foo": "bar"  
    }  

  
So what is the solution? **using a retention count**. That is, when traversing the string down, every time we find a '}' we add 1 to the retention count and every time we find a'{' subtract 1.  
  
We initialise the retention count at -1, as we are currently at the enclosing '}' of the user object. (you may have notice here that when the retention count is -1 on the '}' the object is a direct child, when it is -2 it is a grandchild etc).  
  
We keep on traversing the string until it reaches 0. At this point we know we have reached the closing '}' of the location object. Below is an example:  
  

def getLocationObject(index):  
    retentionCount = -1  
    while retentionCount != 0:  
        if pages\[index\] == "}":  
            retentionCount += 1  
        elif pages\[index\] == "{":  
            retentionCount -= 1  
        index += 1  
    index -= 1;  
    endIndex = index  

  
To get the opening '{' we do the exact same thing, but instead of traversing forwards. We traverse backwards. The example shows how to get the start and end index of the location object and extract it:  
  
  

def getLocationObject(index):  
    retentionCount = -1  
    while retentionCount != 0:  
        if pages\[index\] == "}":  
            retentionCount += 1  
        elif pages\[index\] == "{":  
            retentionCount -= 1  
        index += 1  
    index -= 1;  
    endIndex = index  
    index -= 1  
    while retentionCount != -1:  
        if pages\[index\] == "}":  
            retentionCount += 1  
        elif pages\[index\] == "{":  
            retentionCount -= 1  
        index -= 1  
    startIndex = index + 1  
    objectJson = pages\[startIndex:endIndex +1\]  
    return json.loads(objectJson)  

  
  
The function regexWay then becomes:  
  

def regexWay(igUserToFind):  
    p = re.compile(r'"user":\\s*({\[^}\]*(("'+igUserToFind+'"))\[^}\]*})',re.DOTALL)  
    for found in re.finditer(p,pages):  
        location = getLocationObject(found.end())  
        print(datetime.datetime.fromtimestamp(int(location\["created_time"\])).strftime('%Y-%m-%d %H:%M:%S'))  

  
Now, in this example we used a retention count. But if it makes more sense to some, two counters could have been used. An 'openingBracketCount' and a 'closingBracketCount'. The biases for each would be set in the same way. But I will leave it to you to figure it out ;-)  
  
That's it!!  

### Conclusion and Results

So what are the results and conclusion? We found that using Regex to filter the Instagram API performs at **least half the speed **as traditional traversals.

  

If you don't believe me? [Here clone the code yourself and do some experiments](https://github.com/RaphAustralia/IgAPIFiltering).  
  
Step1: Remember to change the variable yourClientId to your own client id.  
Step2: Run the program using Python interactive mode.  
  
Run the program using interactive mode

  

python -i IgAPIFiltering.py  

  
and try the program by typing timeRegexWay(\[user\_id\]) and timeIterateWay(\[user\_id\])  
  

>>\> timeIterateWay("3419631")  
2012-03-22 13:52:11  
2011-12-29 13:51:52  
2011-12-28 13:38:22  
0.0230000019073 seconds for iteration  
>>\> timeRegexWay("3419631")  
2012-03-22 13:52:11  
2011-12-29 13:51:52  
2011-12-28 13:38:22  
0.00400018692017 seconds for regex  

  
Thanks for reading. Have a good day :)