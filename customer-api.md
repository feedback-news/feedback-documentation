**Feedback Org - Appearance API**
----
  _This API enables a logged user to fetch all appearances and get appearance details from feedback.org database._

* **IDENTIFIER**
    First you need to ask Feedback Org team for a unique token you will add to the header of each API call you make.
    A token take the form of `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`

### Fetch all appearances

* **URL and Method**

  `https://api.feedback.org/appearances`
  Method : `GET`

*  **URL Params**
   **Optional:**

   `page : [alphanumeric]` : page of the list
   `paginator : [alphanumeric]` : number of appearances per page
   `startDate : [string - YYYY-MM-DD]` : starting publication date of appearances
   `endDate : [string - YYYY-MM-DD]` : last publication date of appearances


* **Success Response:**
  * **Code:** 200
    **Content:**
    ```json
    [{
        "id": "FOO",
        "publishedDate": "2020-04-06T12:25:29Z",
        "url": "https://www.url.com/"
    },
    {
        "id": "BAR",
        "publishedDate": "2020-03-08T19:53:26Z",
        "url": "https://www.second-url.com"
    }
    ```
* **Error Response:**

  * **Code:** 401 UNAUTHORIZED
    **Content:** `{"message": "a valid token is missing"}`

  OR

  * **Code:** 400 ERROR
    **Content:** `{ Bad argument : "XXX" }`

* **Url example:**

  Simple call : `https://api.feedback.org/appearances`
  Call with all parameters : `https://api.feedback.org/appearances?page=1&paginator=100&startDate=2020-01-01&endDate=2020-03-31`

* **Sample Call:**

     Here is a snippet to call the API using Python 3 requests
     `pip3 install requests`

    ```
    import requests
    import json
    headers = {'x-access-tokens': <your-token>}
    r = requests.get('https://api.feedback.org/appearances', headers=headers)
    ```


### Fetch one appearance

* **URL and Method**

  `https://api.feedback.org/appearances/<appearance-id>`
  Method : `GET`

*  **URL Params**
   **Required:**

   `appearance-id=[integer]`

* **Success Response:**

  * **Code:** 200
    **Content:**
    ```json
    {
        "claimReviewed": "5G impairs oxygen affinity of hemoglobin",
        "id": "AM",
        "publishedDate": "2020-03-08T19:53:26Z",
        "publisher": null,
        "reviews": [
            {
                "author": "Health Feedback",
                "reviewRatings": [
                    {
                        "alternateName": "Incorrect",
                        "bestRating": 5,
                        "ratingValue": 1.0,
                        "standardForm": "Incorrect",
                        "worstRating": 1
                    }
                ],
                "reviewUrl": "https://healthfeedback.org/claimreview/conspiracy-theorists-claim-that-5g-increases-vulnerability-to-covid-19-with-baseless-theory-that-it-affects-hemoglobin/"
            }
        ],
        "url": "https://www.youtube.com/watch?v=v0-6JTr2Ifo"
    }
    ```

* **Error Response:**

  * **Code:** 401 UNAUTHORIZED
    **Content:** `{"message": "a valid token is missing"}`

  OR

  * **Code:** 404 NOT FOUND
    **Content:** `"global": ["La page que vous recherchez n'existe pas"]`

* **Url example:**

  Simple call : `https://api.feedback.org/appearances/AM`

* **Sample Call:**

     Here is a snippet to call the API using Python 3 requests
     `pip3 install requests`

    ```
    import requests
    import json
    headers = {'x-access-tokens': <your-token>}
    r = requests.get('https://api.feedback.org/appearances/<appearance-id>', headers=headers)
    ```
