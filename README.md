from sklearn.feature_extraction.text import TfidfVectorizer
import pandas as pd
document_Speech_1 = "The car is driven on the road"
document_Speech_2 = "The truck is driven on the highway"

corpus = [document_Speech_1, document_Speech_2]
vectorizer = TfidfVectorizer(stop_words='english')
X = vectorizer.fit_transform(corpus)
feature_names = vectorizer.get_feature_names_out()
df = pd.DataFrame.sparse.from_spmatrix(X, columns=feature_names)    
#Display First F+ew Columns and Last Few Columns
print(df.head())




import requests
from requests_oauthlib import OAuth1
API_KEY = "HdFEGVpqCaSo8C369tL036jgo"
API_SECRET = "ZU745ti0Zzd2qeFqNvsFe9BsMkerNtHsQQOci0E32zlv3o4YR0"
ACCESS_TOKEN = "1904773650232074240-YawiR8JLQMYNem83ZLn891dfjPQXd1"
ACCESS_TOKEN_SECRET = "GvyjAvaW3XPE7Y7bVA3yj7mT6axLh4PQqVIUSMSHcPPLP"

# OAuth1 authentication
oauth = OAuth1(API_KEY,client_secret=API_SECRET,resource_owner_key=ACCESS_TOKEN,resource_owner_secret=ACCESS_TOKEN_SECRET)
while True:
    print("1 - Post a tweet")
    print("2 - Delete a tweet")
    print("3 - exit ")
    option = int(input("select option : \n"))

    if (option==1):
            # Send POST tweet request
            message = input("Enter a tweet mesage : ")
            payload = {"text": message}
            # API endpoint to create tweet
            endpoint = "https://api.twitter.com/2/tweets"
            response = requests.post(endpoint, auth=oauth, json=payload)
    print("Response : ", response.text,"\nCheck your message is deleted from Twitter profile page\n")

        # Send DELETE request
    if (option==2):
        tweet_id = int(input("Enter created tweet ID : "))
                    # API endpoint to delete
        endpoint = f"https://api.twitter.com/2/tweets/{tweet_id}"
        response = requests.delete(endpoint, auth=oauth)
    print("Response : ", response.text,"\nCheck your message is deleted from Twitter Profile page")

            # TO Exit
    if (option==3):
        exit()
            # TO Handle Invalid option
        case
    print("Please select valid Option\n")




    import requests
def get_user_info(username, token):
    url = f"https://api.github.com/users/Kiruthika175"
    headers = {"Authorization": f"Bearer {token}"}
    response = requests.get(url, headers=headers)
    if response.status_code == 200:
        user_data = response.json()
        print(f"User: {user_data['login']}")
        print(f"Name: {user_data.get('name', 'Not available')}")
        print(f"Followers: {user_data['followers']}")
        print(f"Public Repositories: {user_data['public_repos']}")
    else:
        print(f"Error: {response.status_code}")

# Replace 'User name' with the GitHub username you want to explore
# Replace 'token' with the personal access token you generated
get_user_info('Kiruthika175', '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')



 import requests
import pandas as pd

def get_user_repositories(username, token):
    url = f'https://api.github.com/users/Kiruthika175/repos'
    headers = {'Authorization': f'token {token}'}
    response = requests.get(url, headers=headers)
    return response.json()

# Replace 'YOUR_USERNAME' and 'YOUR_TOKEN' with your GitHub username and token
repositories = get_user_repositories('Kiruthika175', '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')

df = pd.DataFrame(repositories)

import matplotlib.pyplot as plt

plt.bar(df['name'], df['stargazers_count'])
plt.xlabel('Repository Name')
plt.ylabel('Number of Stars')
plt.title('GitHub Repository Stars')
plt.xticks(rotation=45, ha='right')
plt.show()



import facebook

access_token = 'EAAZAXqyhgiB0BOZBDAYzZBeaZCkUVVjzPAEsgKOrdKawy58yZC2FlfUVpunwOC7nOj4QbuKCGk0RWl2lHGSNvq1qPYW0D7kdolcjUbVhZCZCZComfZBxMknOFXO9kQsSnyvNx8Rfc37cZC7o5ZAotRRna6V8dVS1ER7r2EIzJfZCZAFvI87woZC8GfzkqfP0frLbrUWZB9Xluc7Q5r5mOX61ZBnb3FmIjyRAurkNsXxEbVT9NvQmX0t8q619A7jZBDpmyWufXpHUZD'

graph = facebook.GraphAPI(access_token)

user_info = graph.get_object('973422088237900')
print("User Info:")
print(user_info)

user_friends = graph.get_connections('973422088237900', 'friends')
if 'summary' in user_friends:
    frdli = user_friends['summary']
    if 'total_count' in frdli:
        frlist=frdli['total_count']
    print("No.of User's Friends is: ",frlist)




import facebook
access_token = 'EAASlE2seyisBO8LlZBDppZCX2B1qpIOqCJ6crmn2qSQkTAQuK8juiDwfToImoiNXwCHR84mwk4dSZCbDtZAjj390rm23mLkNKZAEySzjvXGRDHwd50GeXi1s3ZBvJ1ueqkStVeGoJh8eNYAdrlOh55rDRqSnZAeZBtJj7ULs5Dfp8RzaiySIu0NayafX6bCzqXGw3De3DBzBOJGDG6pcrJRqiVHZAUFhJ'
graph = facebook.GraphAPI(access_token)
page_id='644097902110125'
msg=' '
while True:
    print("1.Publish a Post")
    print("2.Delete a post")
    print("3.Exit")
    ch = int(input("Enter a options:\n"))
    if ch == 1:
        post=input("Enter a post:\n")
        if post==' ':
            print("Post cannot be empty")
        else:
            msg = graph.put_object("me","feed",message=post)
            print("Posted Successfully!")
            print("Your post id is ")
            posts = graph.get_connections(page_id, 'posts')
            if 'data' in posts:
                for post in posts['data']:
                    print(f"Post ID: {post['id']}")
                    msg=str((post['id']))
    elif ch == 2:
        if msg==' ':
            print("It doesn't have Post.")
        else:
            try:
                m=graph.delete_object(msg)
                print("Post successfully deleted!")
            except facebook.GraphAPIError as e:
                print(f"Error: {e}")
    elif ch == 3:
        break
    else:
        print("Invalid options")


